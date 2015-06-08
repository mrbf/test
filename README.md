# Git Large File Storage [![Build Status](https://travis-ci.org/github/git-lfs.svg?branch=master)](https://travis-ci.org/github/git-lfs)

Git LFS is a command line extension and [specification](docs/spec.md) for
managing large files with Git. The client is written in Go, with pre-compiled
binaries available for Mac, Windows, Linux, and FreeBSD.

## Features

By design, every git repository contains every version of every file. But
for some types of projects, this is not reasonable or even practical.
Multiple revisions of a large file take up space quickly, slowing down
repository operations and making fetches unwieldy.

Git LFS overcomes this limitation by storing the metadata for large files in
Git and syncing the file contents to a configurable [Git LFS
server](docs/api.md). Some of the key features include:

* Tight integration with Git means you don't have to change your workflow after
the initial configuration.

* Large files are synced separately to a configurable Git LFS server over HTTPS,
so you are not limited in where you push your Git repository.

* Large files are only synced from the server when they are checked out, so your
local repository doesn't carry the weight of every version of every file when it
is not needed.

* The meta data stored in Git is extensible for future use. It currently
includes a hash of the contents of the file, and the file size so clients can
display a progress bar while downloading or opt out of a large download.

* Clients and servers can make use of all the features of HTTPS, such as caching
content locally on a CDN, resumable uploads and downloads, or performing
requests in parallel for faster transfers.

See the [ROADMAP](ROADMAP.md) for other planned and desired features.

## Known Implementations

- [GitHub.com](https://github.com/early_access/large_file_storage) (support coming soon!)
- [github/lfs-test-server](https://github.com/github/lfs-test-server) (reference server implementation)

## Getting Started

Download the [latest client][rel] and run the included install script.  The
installer should run `git lfs init` for you, which sets up Git's global
configuration settings for Git LFS.

[rel]: https://github.com/github/git-lfs/releases

### Configuration

Git LFS uses `.gitattributes` files to configure which are managed by Git LFS.
Here is a sample one that saves zips and mp3s:

    $ cat .gitattributes
    *.mp3 filter=lfs -crlf
    *.zip filter=lfs -crlf
