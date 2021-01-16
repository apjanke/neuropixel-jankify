# Neuropixel Jankification ideas

## Code and repo organization

* Subfolder(s) for code root paths, instead of putting the root of the project itself on the Matlab path
* Example code (`trialDataExample.m`) in another code root folder, instead of at the root of the project
* Split the [packaged external dependencies](https://djoshea.github.io/neuropixel-utils/acknowledgements/) (libs from File Exchange) into a separate `lib/` directory, to make upgrading/upstreaming them easier
* A `doc-project` directory for maintainer-oriented documentation, like the `build_docs_readme.txt`, and style guides and Release Checklistswe could add

## Packaging and distribution

* Switch to semantic versioning?

## API

* Use lowercase names for packages, per Matlab convention
* `+neuropixel/+internal` package for internal-use (non-public-API) functions
* A `neuropixel.globals` class for lib-wide things, like getVersion(), distroot(), global settings, user prefs, env var discovery, and so on?
