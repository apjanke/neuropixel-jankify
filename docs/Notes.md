---
layout: default
---

Miscellaneous notes about my work.

## Requires Linux and bare metal

This software is Linux-only, and requires a bare metal machine, or an enterprise-grade VM, and an NVIDIA GPU! This is because:

* Kilosort uses CUDA, which requires an NVIDIA GPP and CUDA access.
* Macs are out because they have AMD graphics cards.
* npxutils uses Unix symlink manipulation commands, so Windows is out.
* Consumer-grade VMs (like VMware for home) do not support CUDA.

You _can_ set up a GPU-enabled Linux VM on Azure and other cloud providers. But in my experience Matlab is basically unusuable over SSH X forwarding or VNC over the public internet. YMMV. (It was usable for me using Microsoft RDP to the Azure Linux VM, but that stopped working after a few hours; no idea why.)

## Live Script Editor is bad on Linux in R2019b

In R2019b on my Linux box (a PC with an AMD 3950x and a GeForce 2080 Super), the Live Script Editor just comes up as a blank black page. Doesn't work.
