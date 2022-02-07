---
title: Making macOS useable
---

I have been living without a laptop for over a year.
Well, not really; I have had "work laptops", but those have changed frequently as I have switched employer or role
within the company.
When I changed jobs and became a consultant again, I wanted a computer that is *home*.
A place where I can have everything configured the way I want it.
A portable workstation that is mine and that I can reformat if things get out of hands.
A computer that I can use to teach myself new skills without worrying about IP conflicts with the customer I am
currently working with.
A device that *I own* that does not have neither Global Protect nor Citrix installed...

## So I bought a MacBook.

I could not justify getting a fully specced M1 Max (not to mention they're out of stock and the ETA keeps getting
pushed).
Instead, I bought myself a more reasonable M1 Pro, with 16 GiB of RAM.
I might come to hate myself when I try to run Minikube on this thing, but so be it.

Thusfar, I am undecided as to whether I like this thing or hate it.
It is really nice to have a laptop again, but I pondered for months whether I should buy a Mac or a computer better
suited for running Linux.
What finally tipped the scales was that I wanted to try macOS again.
I used to have a MacBook (the white unibody model from 2008) and I loved it.
Granted, back then I was in music school and predominantly used my laptop for recordings and sheet music writing, but eh.
If worst comes to worst I guess I'll need to buy a real laptop as well.

## Keycodes

My immediate problem with macOS was the keyboard.
Don't even get me started about `⌘` and `^`, I really don't see the point... my biggest issue is that Apple has
made weird decisions about certain keycodes.

For instance, on a regular ISO Keyboard, you create curly braces `{` and `}` by pressing `AltGr + 7` and `0`
respectively.
That is awful and not particularly ergonomic, but what matters are they keycodes that are being sent from the keyboard
to the operating system.
Knowing your keycodes is key (pun intended) when you want to program your own keymaps.

I have been using the [Svorak A5 layout](http://aoeu.info/) for almost 10 years and after tweaking certain buttons
here and there I really like my layout.
Furthermore, I have two [crkbds](https://github.com/foostan/crkbd) (which run
[QMK](https://github.com/qmk/qmk_firmware)).
If you look at the physical layout of the crkbd, you realize that there's no number row.
Hence, in order to write any special characters, you must use layers.
In my *special character layer*, I have used the keycode corresponding to `AltGr + 7` and mapped it to `{`.
It works like a charm (in Windows and Linux) and I have been rocking the same (ish) QMK layout since I got my first
programmable keyboard back in 2014.

When I pluged my crkbd into my new Mac, I noticed that a handful of keys were not working properly.
In particular, I have found that Apple uses different keycodes for the following characters: `{`, `}`, `|`, `<`, `>`
and `\`. 
I really wanted to avoid having different layers for macOS and [Windows / Linux] on my keyboard, especially since I
have two crkbds and try my best to keep them in sync.
Luckily, I found [Ukelele](https://software.sil.org/ukelele/), a software that helps you edit macOS keymaps.
With this tool I could open up the default Swedish keymap on macOS and create a *Swedish Windows-ified* version, where
the characters mentioned above are mapped to keys yielding the same keycodes as my crkbd expects.

You can find my crkbd layout
[HERE](https://github.com/ErikThorsell/qmk_firmware/blob/master/keyboards/crkbd/rev1/common/keymaps/svorak_a5/keymap.c).

## Repeating keys

In the Settings application, you can decide whether to allow key repetition:

<p align="center">
  <img width="150" src="{{ site.url }}/assets/images/apple-settings-key-repeat.png">
</p>

but this setting only applies to non-alpha-numerical characters.

Wut?

The idea seems to be that you should be able to repeat certain keys, while still use macOS' *"press down some letters
and get the option to add some quirks to it"-feature*.

<p align="center">
  <img width="150" src="{{ site.url }}/assets/images/apple-key-long-press.webp">
</p>

I don't want that feature!

Luckily, it seems that you can enable proper key-repetition behavior with this command:

```
defaults write -g ApplePressAndHoldEnabled -bool false
```

I have yet to try it (because it requires a restart of the laptop and I'm writing this post now) but hopefully it works
out.

## Tiling windows

Tiling window managers made an entrance in my life when I discovered [Openbox](https://en.wikipedia.org/wiki/Openbox)
almost 10 years ago.
I really liked the efficiency of the WM and it wasn't long until I found [i3](i3wm.org/) which I have been using for several years.
I ran i3 on my previous laptop and I really want to get something similar for my new Mac.

I have looked around online and I have found more basic managers, like [Moom](https://manytricks.com/moom/), and more
advanced programs like [Amethyst](https://github.com/ianyh/Amethyst).
Unfortunately, I have not been particularly impressed by either.
It would be enough to find something equivalent to
[Fancy Zones](https://docs.microsoft.com/en-us/windows/powertoys/fancyzones) that you get in Windows' PowerToys, but I
have not found that either.

It might come down to macOS simply not being well suited for tiling.
The OS seems heavily invested in fullscreen applications (pressing the green button and getting a dedicated
desktop for the app), so maybe I just need to learn how to use that instead.

## That's it for now

Expect more updates going forward...

Any tips to become more productive using macOS?
Please let me know!
