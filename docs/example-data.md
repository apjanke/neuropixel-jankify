---
layout: default
title: Example Data
---

Neuropixel Utils is a library for processing brain imaging data, which can be quite large. This presents a challenge, because on the one hand we want to have example data readily available, and on the other hand it's big, so it's hard to store and transmit.

It's important to have a canonical set of example data available to both developers and users of the Neuropixel Utils library, so that during development, tests can be run against a standard set of inputs, and for users, they can run example code against a standard, known-good set of example inputs.

I don't have a good answer to this yet, but here are my thoughts.

## Requirements and Desires

I think we want:

* A single collected set of example input data sets
* Available on the internet in a central, public location
  * So we don't have to rely on devs and users passing around files person-to-person
* Version-controlled
  * So the example data set can be kept in sync with the library that is using it, and we can track changes to the example data
* Cloud-hosted
  * Because who wants to sysadmin a file hosting site?
* Would be nice to have a data set small enough to use it inside CI

## Options

The ideal solution seems to me to be a Git or other source control repo that tracks a history of the full collection of example data. Git LFS would make it practical to store large binary files in Git.

Finding somewhere to host it is the problem. The files Neuropixels deals with can be 30 GB or larger. Even if you want to pay for it, that presents a problem for most Git hosting providers.

* GitHub has a limit of 2 GB per file for Git LFS
* Atlassian Bitbucket, even on paid accounts, has a limit of 10 GB per file for Git LFS
* GitLab doesn't like my uploads of the 30 GB "Vinnie" Imec data set, though I couldn't find documentation of what their file size limit is.

This sounds wackdoodle, but Microsoft Azure DevOps might actually be a viable choice here? Azure has huge storage limits compared to the above Git hosting providers.

## Thoughts

Even if we find a good hosting solution, using full-size input files in a CI service is probably going to be a no-go, because CI runs typically have to re-download all their data each time.

The real solution here is probably to get trimmed-down example input data sets: files that are too small to be useful for real work, but are in a valid format so it exercises the code, and are small enough to be passed around between developers and users.
