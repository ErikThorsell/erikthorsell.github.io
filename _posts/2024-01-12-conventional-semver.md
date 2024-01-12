---
title: Conventional Semver
---

A successful company is able to provide a monetised solution to a user’s
problem.
That seems easy enough, but how do you know whether you're building what your
users want?
I believe we figure this out by asking them, meaning that the sooner we can put
_something_ in the hands of our users, the sooner we will know whether we're on
the right track or not.

This is why I am a big proponent of trunk-based development; the way-of-working
that emphasises fast integration to a shared branch.
If everyone in your organisation strive to make it easy to deliver new versions
of your product to your users, you will get an answer to the above question
sooner.

I have helped several organisations "work trunk-based" over the past couple of
years, but I have always had to reinvent the wheel when it comes to the tooling
used for automating the versioning of the product.

## Now, there's a tool for that!

[Conventional Semver](https://github.com/ErikThorsell/bump-semver-using-conventional-commits)
is a small Python CLI which takes a SemVer tag and a Conventional Commit
message as input, and returns "the next version".
Both [SemVer](https://semver.org/) and [CC
messages](https://www.conventionalcommits.org/) are well described by their
respective standards -- and the only thing my tool does is glue together
existing parsing libraries -- but finally I don't have to rewrite the same
scripts for every new assignment!

<p align="center">
  <a href="https://github.com/ErikThorsell/bump-semver-using-conventional-commits">
    <img src="{{ site.url }}/assets/images/conventional_semver-social.jpg">
  </a>
</p>

The tool is FOSS and available on [PyPi](https://pypi.org/project/conventional_semver/).
You're more than welcome to use it and contribute!

## Usage

_The [README.md on GitHub](https://github.com/ErikThorsell/bump-semver-using-conventional-commits)
contains all the info you need, I hope, but here's the gist._

```shell
$> pip install conventional_semver

# If your latest tag is 1.7.2 and
# your latest commit message "feat: add new shiny thing"
$> conventional_semver \
  --semver "$(git describe --abbrev=0 --tags)" \
  "$(git log -1 --pretty=%B | tr -d '')"

1.8.0

# Or, doing everything manually:
$> conventional_semver --semver 1.7.2 "feat: add new shiny thing"

1.8.0
```

## But there's more!

I have created [a dotnet sample project](https://github.com/ErikThorsell/conventional_semver-test)
where you can [see the CLI in action](https://github.com/ErikThorsell/conventional_semver-test/blob/main/.github/workflows/main.yml).

<!-- --------------------------------------------------------------------------------------------------------------- -->

<!-- FEET NOTES -->
[^footnote]: Text goes here

<!-- REFERENCES -->
[reference]: https://example.com