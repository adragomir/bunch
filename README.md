你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# bunch

An npm-like tool for easily managing Go (golang) dependencies.

[![Release](https://img.shields.io/github/release/dkulchenko/bunch.svg)](https://github.com/dkulchenko/bunch/releases)
[![Build Status](https://img.shields.io/travis/dkulchenko/bunch.svg)](https://travis-ci.org/dkulchenko/bunch)

## Overview

`go get` is very good. But managing multiple packages, locking versions down for reproducible builds, and 
changing GOPATH or rewriting package imports is an exercise left to the developer. bunch tackles this
issue by providing a comprehensive tool for managing Go dependencies similar to npm for Node, supporting
installing, uninstalling, pruning, listing outdated packages, and much more.

## Installation

```
go get github.com/dkulchenko/bunch
```

Alternatively, [precompiled binaries](https://github.com/dkulchenko/bunch/releases) for 
supported operating systems are available.

You can pin bunch itself, if you'd like to lock the version of bunch down. If bunch finds a version 
of itself in the vendored environment (that is, .vendor/bin/bunch exists), it will use that version instead.

## Bunchfile

See this [repo's Bunchfile](https://github.com/dkulchenko/bunch/blob/master/Bunchfile) as an example.

```
github.com/this/repo !self

# comments are fun!
github.com/another/package
github.com/another/package2 v2 # can be a branch, tag, or commit
github.com/another/package3 a2b5va78d

github.com/another/package4 >= 1.0
github.com/another/package5 ~> 1.4.x
github.com/another/package6 > 1.0, < 1.4
```

## Usage

### Managing packages

(optional) Generate a Bunchfile based on your existing imports to get you started:

```
bunch generate
```

Install all packages listed in Bunchfile to .vendor directory:

```
bunch install
```

Install a specific package and save it to the Bunchfile:

```
bunch install github.com/abc/xyz
bunch install github.com/abc/xyz --save
bunch install github.com/abc/xyz@v2 --save
bunch install github.com/abc/xyz github.com/abc/xyz2
```

Update all packages to latest versions matching Bunchfile:

```
bunch update
```

Remove a package and save the change to the Bunchfile:

```
bunch uninstall github.com/abc/xyz
bunch uninstall github.com/abc/xyz --save
```

Prune unused packages from vendor directory (similar to npm prune):

```
bunch prune
```

List outdated packages:

```
bunch outdated
```

Lock down the commits currently in use (creates Bunchfile.lock; similar to npm shrinkwrap):

```
bunch lock
```

Rebuild (recompile) all packages:

```
bunch rebuild
```

### Using the vendored environment

Run commands/builds within the vendored environment (sets $GOPATH and $PATH):

```
bunch go build .
bunch go fmt
bunch exec make
bunch shell
```

You can also add this to your .bash_profile to make the `go` command automagically be bunch-aware (e.g. go build will automatically have the correct $GOPATH set if a Bunchfile is present): 

```
if which bunch > /dev/null; then eval "$(bunch shim -)"; fi
```

## Limitations

For basic operations like installing/uninstalling/updating/pruning packages, all VCSes supported by `go get` are supported by bunch (git, hg, svn, and bzr).

For more advanced operations, packages using Git are fully supported. Mercurial has mostly full support (does not support version ranges in the Bunchfile). Bazaar has some support (does not support version ranges, "bunch outdated", or "bunch install" caching up-to-date packages). Subversion has rudimentary support (only install/update/uninstall/prune).

## Contribute

Patches welcome :)

- Fork repository
- Create a feature or bugfix branch
- Open a new pull request

## License

The MIT License (MIT)

Copyright (c) 2015 Daniil Kulchenko <daniil@kulchenko.com>
