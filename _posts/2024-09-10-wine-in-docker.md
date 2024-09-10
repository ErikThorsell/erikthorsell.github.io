---
title: Install a GUI application in Docker using Wine
---

Here's a post I never thought I'd write...

I'm currently working with a client who has a very extensive support agreement with their users.
The client develops embedded software for a plethora of different PLCs and because of this it's not always super easy to
find compilers.
(Or, it's rather the case that the company that makes the PLC also creates a compiler and you need both in order to
create your product.)
Because of the way my client offer support, they must ensure that they can build and patch their software for years to
come.
It is not infeasible that my client will need to re-build and patch a product they released back in 2010.
So how do I help my client make sure they can do this?

Over the past couple of years -- and long before I came into the picture -- the client has built a very good build
system based on Docker.
In essence, the build system checks a config file in the product's repository, downloads the appropriate Docker images
and executes the build/test commands specified in the config.
Any solution I come up with must be compatible with this way of working.
I have therefore spent the past couple of days creating a new Docker image + config to build yet another (old) product.

# Windows. For real?

When my client told me that _part of_ the build included a compiler which only runs on Windows, my heart stopped a
little.
Note the _part of_.
The product is cross-compiled, makes use of compilers that only run on Linux and uses one compiler which only runs on
Windows -- _yay_!

A predecessor of mine had configured a way of building this project in a Linux environment using
[Wine](https://www.winehq.org/) for the Windows compiler and my instructions from the client were clear:

> Try to replicate the old build system as closely as possible!

So... the task was to create a Docker image and a build config, capable of running both the Linux compilers _and_ the
super old Windows-only compiler.

# Wine in Docker

The first thing I did was to check whether anyone else had been crazy enough to attempt this already.
Naturally, someone had -> [scottyhardy/docker-wine](https://github.com/scottyhardy/docker-wine/blob/master/Dockerfile).

I looked through Scotty's code and borrowed the Wine installation step he cooked up:

```YAML
# Install Wine
RUN wget -nv -O- https://dl.winehq.org/wine-builds/winehq.key | APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1 apt-key add - \
    && echo "deb https://dl.winehq.org/wine-builds/ubuntu/ $(grep VERSION_CODENAME= /etc/os-release | cut -d= -f2) main" >> /etc/apt/sources.list \
    && dpkg --add-architecture i386 \
    && apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --install-recommends winehq-stable \
    && rm -rf /var/lib/apt/lists/*
```

Thereafter I needed to figure out how to install the Windows compiler.
Naturally, the compiler cannot be installed headless but makes use of an install wizard in which you must click: `Next >
Next > Next > ...`.
How do you do that while building a Docker image?

Well, you use [Xvfb](https://en.wikipedia.org/wiki/Xvfb) to create a virtual framebuffer in your build process and open
Wine inside of it, in order to trick the installer that it's actually running in a GUI and that someone is repeatedly 
clicking along in the wizard.

```YAML
ENV DISPLAY=:0
RUN xvfb-run --auto-servernum --server-args="-screen 0 1024x768x16" bash -c \
    "wine /opt/compiler.exe & \
    pid=\$! && while kill -0 \$pid 2> /dev/null; do \
    xdotool key Return; \
    echo 'Pressed Enter'; \
    sleep 15; \
    done && wait \$pid && echo 'Wine process finished'"
```

In Swedish, you can say that you "do violence" on something, and I think this is exactly what that expression is meant
to be used for.
I feel like I have done violence on both Docker and Wine and the poor compiler.
But it works(!) and the client is happy.
