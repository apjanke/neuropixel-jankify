---
layout: default
---

## Naming and prose style

* Do you prefer "data set" or "dataset" when talking about IMEC and Kilosort data sets? ("dataset" might be confused with the Matlab `dataset` type/class.)
* Do you prefer "IDs" or "Ids" or "ids"?

## Code

* You've got some calls to `debug()` scattered around the example code. It's broken because that function doesn't exist. Would you like me to add some real logging support?
  * I'd recommend basing it on a "privatized" vendored version of my [SLF4M Logging Framework for Matlab](https://slf4m.janklab.net).
* Do you want to try to be Mlint-inspection-clean?

## Example code and data

* The workflows in the examples and tutorial are non-idempotent! They write back to the original input files. This means they'll produce different results if run more than once, and would produce changes that could get checked back in to an example data set repo.

## Miscellaneous

* Requires a Linux box (and a bare-metal one at that). Let's add Windows support!
  * CUDA = NVIDIA, so no Macs for Kilosort. And npxutils uses Unix symlink commands, so no Windows.
* [Kilosort2.5](https://github.com/MouseLand/Kilosort/releases/tag/v2.5) is out, and Kilosort3 is [under development](https://github.com/MouseLand/Kilosort). Want to add support for them?
