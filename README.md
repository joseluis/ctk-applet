# ctk-applet

Run archived [Cut-the-Knot] Java applets locally from their original web pages.

Give `ctk-applet` a Cut-the-Knot page URL, and it will find the applets on that page,
prepare a local launcher file, and open the selected applet with Java's `appletviewer`.

[Cut-the-Knot]: https://www.cut-the-knot.org

## Contents

- [What this is for](#what-this-is-for)
- [What most users need](#what-most-users-need)
- [Requirements](#requirements)
- [Install Java 8](#install-java-8)
- [Install ctk-applet](#install-ctk-applet)
- [Quick start](#quick-start)
- [How selection works](#how-selection-works)
- [Commands](#commands)
- [What each command does](#what-each-command-does)
- [FAQ](#faq)
- [Acknowledgements](#acknowledgements)

## What this is for

This tool is for old Java applets from the Cut-the-Knot archive.

Because these applets use the old Java applet system, you need a **Java 8 JDK**
with `appletviewer`. A newer JDK is not enough.

## What most users need

1. Install **Java 8 JDK**
2. Make sure `appletviewer` works from a terminal
3. Download `ctk-applet`
4. Run:

    ctk-applet setup
    ctk-applet run https://www.cut-the-knot.org/ctk/May2001.shtml --name SilverDollar

## Requirements

* Java 8 JDK
* `appletviewer` available in `PATH`

## Install Java 8

Install a Java 8 JDK that still includes `appletviewer`.

### Linux

Use your distribution packages when available.

Ubuntu/Debian:

    sudo apt install openjdk-8-jdk

Arch Linux:

    sudo pacman -S jdk8-openjdk

Fedora:

    sudo dnf install java-1.8.0-openjdk-devel

openSUSE:

    sudo zypper install java-1_8_0-openjdk-devel

You can also use SDKMAN instead of system packages:

    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    sdk list java
    sdk install java 8.0.482-tem

### macOS

With Homebrew:

    brew install --cask temurin@8

Or with SDKMAN:

    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    sdk install java 8-tem

### Windows

Install a Java 8 JDK such as Eclipse Temurin 8, then make sure `appletviewer`
is available in `PATH`.

## Install ctk-applet

Download the binary for your platform from the [Releases] page.

If you already have [Rust installed], you can also run the script directly.

[Releases]: https://github.com/joseluis/ctk-applet/releases
[Rust installed]: https://rust-lang.org/tools/install/

## Quick start

Prepare the local Java class archive once:

    ctk-applet setup

List the applets found on a page:

    ctk-applet list https://www.cut-the-knot.org/ctk/May2001.shtml

Show details for one applet:

    ctk-applet show https://www.cut-the-knot.org/ctk/May2001.shtml --index 1

Run one applet directly from the page URL:

    ctk-applet run https://www.cut-the-knot.org/ctk/May2001.shtml --name SilverDollar

Save launcher files for later use:

    ctk-applet save https://www.cut-the-knot.org/ctk/May2001.shtml --all

Run a previously saved launcher:

    ctk-applet run-file saved/may2001/02-SilverDollar.html

## How selection works

If a page contains exactly one applet, `show`, `save`, and `run` can be used
without `--index` or `--name`.

If a page contains several applets, choose one explicitly with either:

* `--index N`
* `--name CODE`

## Commands

    ctk-applet setup
    ctk-applet list <url>
    ctk-applet show <url> [--index N | --name CODE]
    ctk-applet save <url> [--all | --index N | --name CODE] [--out-dir PATH]
    ctk-applet run <url> [--index N | --name CODE]
    ctk-applet run-file <path>

## What each command does

* `setup` downloads `classes.zip` when needed and extracts the local `classes/` directory
* `list` shows the applets found on a page
* `show` prints the applet information for one selected applet
* `save` writes launcher HTML files to `saved/<page-slug>/`
* `run` creates a temporary launcher file and opens it with `appletviewer`
* `run-file` opens a previously saved launcher file

## FAQ

### Is this an official Cut-the-Knot tool?

No. `ctk-applet` is an independent utility and is not affiliated with or endorsed by Cut-the-Knot.

I came to Cut-the-Knot while looking into take-away game variations
and found a remarkable collection of games, applets, and mathematical writing.
But the archived applets were no longer easy to run, and it was clear from
user discussions that many people did not know how to make them work locally.

This tool was made to help bridge that gap: a small, reliable, and easy-to-use
way to run those applets again from their original page URLs.

### Why do I need Java 8?

These applets use the old Java applet system and need `appletviewer`,
which is part of a Java 8 JDK. A newer JDK is not enough here.

### Why do I need to run `ctk-applet setup`?

`setup` prepares the local `classes/` directory used by many archived applets.

### `appletviewer` is not found. What should I check?

Make sure you installed a **Java 8 JDK**, not just a JRE or a newer JDK,
and that `appletviewer` is available in `PATH`.

### Does this download the applet class files from Cut-the-Knot?

It uses the published Cut-the-Knot Java class archive,
which mirrors the site's historical `classes/` directory.
For background, see [Help with Java].

[Help with Java]: https://www.cut-the-knot.org/HelpWithJava.shtml

### Will saved launcher files keep working?

Yes, as long as the local `classes/` directory stays in place relative to them.

## Acknowledgements

With appreciation for Cut-the-Knot and for the work of Alexander Bogomolny,
whose writing and interactive applets made mathematics unusually vivid and approachable.
