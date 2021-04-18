---
layout: default
---

This document describes the suggested changes I've come up with for the Neuropixel Utils library and its project repo.

## Where's the code

Because I ended up making extensive changes to various aspects of the library and repo that are all intertwined, I decided to make a separate repo and just do all the changes there, instead of structuring the changes as PRs from a fork repo. Once the code work for this project is complete, _then_ I'll present that to Dan, he can choose what changes he likes and doesn't, and I'll package the ones he likes up as PRs to the main neuropixel-utils repo. That will save some work, make it easier to review the changes, and keep the upstream repo's commit history tidy.

My work-in-progress version of the repo is at <https://github.com/apjanke/npxutils-apj-wip-01>. Commentary on it can be found at <https://github.com/apjanke/neuropixel-jankify>. A live preview of the updated GitHub Pages site is at <http://npxutils-wip.apjanke.net/>.

## Repo structure

I've changed the repo layout, moving things around and introducing new top-level directories and files. This is mostly to support doing true versioned releases of Neuropixel Utils.

A versioned release is a specific version of the library that is packaged and distributed as archive files (zip files, tarballs, and/or Matlab Toolbox .mltbx files). Versioned releases are desirable for several reasons: They let you identify known-good, ready-for-production versions of the repo, and distinguish them from ongoing, possibly-unstable work on the head of the main branch. This lets users get stable versions of the library. Plus it lets them succinctly communicate to other users which version of the code they used to do some work, which is important for reproducible research. And it's easier for many users to download a distribution file and install from that than cloning a Git repo. Distribution files play nicely with package managers and software deployment tools. And they can be readily archived by users, sysadmins, and archivists.

The new release-packaging-oriented package structure is based on my [MatlabProjectTemplate](https://matlabprojecttemplate.janklab.net/) project from [Janklab](https://janklab.net/).

I also rearranged things so that the GitHub Pages site is deployed in the `docs` directory of the main branch, instead of on a separate `gh-pages` branch. For nontrivial sites, the `gh-pages` deployment model is harder to work with: you can't readily view the entire site build process without hopping around in your Git history. More importantly, doing it on the `main` branch allows us to package a copy of the documentation with the release distributions. This provides a local copy of the documentation, ensuring that users are looking at the correct version of the documentation for the version of the code they are running, and allows it to be pulled in to the Matlab Toolbox for viewing in the Matlab Help Browser.

All the documentation files had to be rearranged to support this.

### Matlab Toolbox support

I added support for building Neuropixel Utils into a [Matlab Toolbox](https://www.mathworks.com/help/matlab/matlab_prog/create-and-share-custom-matlab-toolboxes.html) and distributing it as an `.mltbx` installer file. I don't know how many users will actually want to use this format, but it's kind of cool, and probably a good look for the project to have. MathWorks will appreciate it, too.

The `.mltbx` file will be included in the release distribution files posted for each release.

### What's new in the repo structure

#### File organization

* `Mcode/` – The Matlab source code itself. This is a separate folder to keep things tidy, and avoid the (unlikely) case of problems from having extraneous files on the path.
* Documentation
  * `doc-src/` – The MkDocs source for the documentation lives here now.
  * `docs/` – This is now the _generated output_ from MkDocs. This is required because "`docs`" is the only subdirectory name that GitHub supports publishing from.
  * `doc-project/` – Internal, developer-oriented documentation for people working on Neuropixel Utils itself.
* `examples/` – User-facing example code is collected here. These examples are also used to generate part of the doco.
* `.mlproject.json`, `info.xml`, `neuropixel-utils.prj.in`, `npxutils_toolbox_info.m` – These are all for Matlab Toolbox packaging support.
* `Changes.md` – [ChangeLog](https://keepachangelog.com/) for the library.

#### Repo meta-organization

* The `gh-pages` branch is deprecated, and will no longer be updated.
* The default `master` branch is [renamed to `main`, for sensitivity reasons](https://sfconservancy.org/news/2020/jun/23/gitbranchname/).
* GitHub Pages is configured to publish from `main` instead of `gh-pages`.

## Library documentation

### ChangeLog

I added a [ChangeLog](https://keepachangelog.com/) to the library at `Changes.md`. This is a manually-maintained, curated history of changes made to the library. It's very useful for users to have this, so they can see what important things have happened in each release.

### Local copies

The MkDocs stuff is now targeting local, in-repo/in-distribution copies of the documentation as well as publishing to GitHub Pages. This is so users (and devs) can have copies of the doco corresponding to the exact version of the code they're working on, and so it can be included in the Matlab Help Browser.

I changed the `mkdocs.yml` config to turn off directory links, in order to support viewing the docs directly from files on the filesystem. This way users don't have to run a web server in order to correctly browse them.

## API changes

I've made some suggested changes to the public API for the library

### Package naming

I renamed the packages to keep in line with Matlab package naming conventions, and make them easier for clients to use. The convention for Matlab (and many other programming languages) is to have package names in all lower case. And in Matlab's case, it's important that they be short: because Matlab's `import` statement is function-scoped, not file-scoped, you're going to end up typing your package names a _lot_. (IMHO this is a design flaw in Matlab's `import` statement.)

I renamed the top `+Neuropixel` package to `+npxutils`. That's short, catchy, and distinctive, and includes the "Utils" part of "Neuropixel Utils": I think that's a good idea, to distinguish this "Neuropixel Utils" library from "Neuropixels" itself, which is the probe manufacturer, and has its own library on GitHub, right?

Renamed `+Utils` to `+utils` and `+DataProcessFn` to `+dataprocess`, to conform with Matlab's naming convention's case.
