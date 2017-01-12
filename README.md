# makenv

Copies nvALT over to a customized bundle to allow multiple instances

## Overview
nvALT only allows one instance to run at a time. So, for example, there is no way to have a "work" set of notes and a "personal" set of notes pointing to different directories and running at the same time.

You can get around this by copying the app bundle and making a few changes to internal config files so that it has its own preferences, url scheme, and so forth. This process is outlined in [this blog post] (http://verifyandrepair.com/03-27-2014/running-multiple-instances-of-nvalt/) by Craig Eley.

However, doing this breaks auto-updating on the copied bundle. The main app will auto-update, but then you have to copy and modify everything all over again. It's a pain to keep up with now that nvALT's development is moving again.

This script automates copying nvALT to a renamed bundle and changes the various things in Info.plist that must be changed to keep the two bundles from colliding with each other. 

You can re-run it from Terminal command line (or Spotlight, after `chmod +x`'ing it) whenever nvALT is updated. The copy's preferences will be preserved when the bundle is recreated in this fashion.

## Usage

Usage, from the header comment:

```
# Copies nvALT over to a customized bundle
#
# makenv [name] [identifier] [url scheme 1] [url scheme 2]
#
# Note that Brett's copyright notice inside the plist is
# changed in the process. This, as well as any identifier
# changes, are purely mechanical and are not meant to in
# any way indicate different ownership of the app.
#
# Please do not redistribute the new copy of the app.
```

`name`: name of the renamed bundle. Original was `nvALT`. Default is `nvGEO`.

`identifier`: this is a namespace used for preferences. Original was `net.elasticthreads.nv`. Default is `com.snarksoft.nvgeo`.

Two bundles with the same identifier share preferences...poorly. If you create more than one nvALT copy make sure to change this to something unique per-copy. 

`url scheme 1`: this is the first url scheme protocol specifier. Original was `nv`. Default is `nvg`.

`url scheme 2`: this is the second url scheme protocol specifier. Original was `nvalt`. Default is `nvgeo`.

As with `identifier`, these should be unique per-instance or else app-to-app launching will misbehave. If you create more than one nvALT copy, make sure to change both of these to something unique per-copy.

**TL;DR: if you don't supply anything you'll get a bundle called `nvGEO.app` with its own `com.snarksoft.nvgeo` preferences namespace and `nvg`/`nvgeo` url schemes.**

## Next Steps

* Add icon handling so that an .icns file can be copied into the new bundle as well.
* Add proper usage and parameter handling
