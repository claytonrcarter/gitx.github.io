---
layout: default
---
[gitx]:    http://gitx.frim.nl/
[git]:     https://git-scm.com/
[dmgsl]:   https://github.com/gitx/gitx/releases/download/0.17/GitX.built.by.Xcode_13.2.1.dmg
[commits]: https://github.com/gitx/gitx/commits/master
[builds]:  https://github.com/gitx/gitx/releases
[bug]:     https://github.com/gitx/gitx/issues?labels=bug
[rfe]:     https://github.com/gitx/gitx/issues?labels=enhancement
[treesl]:  https://github.com/gitx/gitx/tree/10.6_snow_leopard

GitX-dev is a fork (variant) of [GitX][gitx], a long-defunct GUI for the
[Git][git] version-control system. It has been maintained and enhanced with
productivity and friendliness oriented changes, with effort focused on making a
first-class, maintainable tool for today's active developers.

[sshot]: images/screenshots/GitX-dev-repo_window.png
[sshotsmall]: images/screenshots/GitX-dev-repo_window-small.png

{:.center}
[![Screenshot: main window][sshotsmall]][sshot]

# Features and Status


For the most up-to-date information, please see the
[change log for the latest build][builds], or the [live commit list][commits].

Building on the solid foundation of GitX, GitX-dev provides:

* History browsing of your repository

* See a nicely formatted diff of any revision

* Search based on author or revision subject

* Look at the complete tree of any revision
  * Preview any file in the tree in a text view or with QuickLook
  * Drag and drop files out of the tree view to copy them to your system

* Support for all parameters git rev-list has

* Good performance on large (200+ MB) repositories

GitX-dev is further specialized for software developers, and is used day-to-day
in production environments. We consider it to be feature-complete for most git
workflows, with only uncommon or potentially-destructive commands requiring
`git` command-line interaction.

As a collaboration tool for a diverse team trying to make other things; we take
feedback seriously from everyone involved in software production. We want to
make good version control an invisible, second-nature step of everyone working
on a product. Re-work sucks.

## How is it better?

[gitx_l]: https://gitx.laullon.com/
[gitx_r]: https://github.com/rowanj/gitx
[sparkle]: http://sparkle.andymatuschak.org/
[issue2]: https://github.com/rowanj/gitx/issues/2
[libgit2]: https://github.com/libgit2/libgit2
[objectivegit]: https://github.com/libgit2/objective-git

GitX-dev includes a selection of improvements from around the GitX fork
community.

* The awesome branch/remote/tag sidebar from [GitX (L)][gitx_l]
* Clickable commit references in blame view
* Many awesome improvements from [GitX (R)][gitx_r]

There are also a range of visible and under-the-hood changes to make GitX-dev a
distinct improvement on other forks you may find.

* Notably better performance on large repositories

* Reliable in-app updates thanks to [Sparkle][sparkle]

* Significantly reduced ([and shrinking][issue2]!) use of `git` command-line
  tool in favor of direct use of [libgit2][libgit2] and
  [ObjectiveGit.framework][objectivegit].

* Lower, more regular memory footprint due to porting to Objective-C Automatic
  Reference Counting

* Improvements to the command-line `gitx` tool

## Does this come at a cost?

Monetarily? No, GitX-dev will always be freely available. But with a limited
number of contributors, and to properly support Mac and iOS devs using the
latest-and-greatest (even beta) environments; there is an obvious need to
reduce the support and maintenance load.

* 64-bit Intel only, building for other targets is left as an exercise to the
  would-be user

* OS X 10.7 Lion and above.

* Not as many graphical niceties as some forks. Many are lacking only because
  of the time it would take to find and merge them; some are omitted by
  conscious decision to keep development focused and the high signal-to-noise
  ratio of the interface

## Where can I get it?

1. Grab the [most recent package][builds].

   * The last build to support OS X 10.6 Snow Leopard is
     [GitX-dev 0.14.81][dmgsl]. Please see
     [my notes on Snow Leopard support in GitX](#os-x-106-snow-leopard-support).

2. Click the *"Check for updates..."* item in the GitX menu. New builds are
   available through in-app update.

GitX-dev uses the [Sparkle][sparkle] framework for in-app updates; so once you
have version 0.11 or later, you can check for or update to new builds from the
GitX menu at any time, or opt-in for automatic updates.

# Development

[gitmodules]: http://book.git-scm.com/5_submodules.html

Developing for GitX-dev has a few requirements above and beyond those for
mainline GitX.

Most third-party code is referenced with Git submodules, so
[read up][gitmodules] on those if you're not familiar.

* Very recent Xcode install, 4.5 release strongly recommended.

* Most development is done on OS X 10.8 Mountain Lion, OS X 10.7 Lion may or
  may not work.

* `CMake` with a working command-line compiling environment for building
  `libgit2`

* `node.js` for building `SyntaxHighlighter` (not necessary unless you're
  updating SyntaxHighlighter itself)

# License

GitX is licensed under the GPL version 2. For more information, see the
attached COPYING file.

# Usage

GitX itself is fairly simple. Most of its power is in the `gitx` binary, which
you should install through the menu. the `gitx` binary supports most of `git
rev-list`'s arguments. For example, you can run `gitx --all` to display all
branches in the repository, or`gitx -- Documentation` to only show commits
relating to the 'Documentation' subdirectory. With `gitx -Shaha`, gitx will
only show commits that contain the word 'haha'. Similarly, with `gitx
v0.2.1..`, you will get a list of all commits since version 0.2.1.

# Helping out

Any help on GitX is welcome. GitX is programmed in Objective-C, but even if you
are not a programmer you can do useful things. A short selection:

* Give feedback
* File [bug reports][bug] and [feature requests][rfe]

## OS X 10.6 Snow Leopard support

I haven't had the ability to test on 10.6 since 2011; GitX support has been
maintained until mid 2013 by virtue of timely bug reports and relatively simple
fixes, but the aggregate support weight to continue targeting 10.6 now exceeds
my threshold for how much I'm willing to jeopardize further feature and
performance development.

If you'd like to see GitX continue to support OS X 10.6, you are most welcome
to fork from the [10.6_snow_leopard][treesl] branch I have published on GitHub
as a starting point.

Regrettably, although I feel the pain of being stranded on an old version, I am
not interested in continuing to support 10.6; I will outline the main reasons
for this here.

* OS X 10.6 does not support ARC `weak` references, complicating memory
  management

* [Objective-Git][objectivegit] no longer supports 10.6 (and is phasing in the
  use of `weak` references)

* *Objective-Git* is presently introducing features like an SSH remote
  transport, which will allow us to further dramatically reduce reliance on
  parsing command-line output of 'git' commands. This and other new features,
  along with their usual stream of bug fixes and performance improvements is a
  substantial reason to not freeze on an old version to continue to support
  10.6.

* OS X 10.6 does not support XPC services at all, and these are one of my main
  avenues of exploration for further increasing performance and
  reliability.

* Many Snow Leopard users seem to be running hardware that can be upgraded to
  10.7 or higher (we've only built for 64-bit Intel for over a year), and have
  just chosen not to do so. I'm not saying that your choice isn't valid, but it
  is a choice.

* If I can't test on 10.6, and I break compatibility in an update, it's broken
  for all 10.6 users until somebody reports it and typically until I fix it. I
  think that's a much worse experience for those 10.6 users than running an old
  but functional and stable build.
