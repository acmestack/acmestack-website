---
title: "Code conventions"
description: "Code conventions"
lead: ""
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "contributing"
weight: 55
toc: true
---

- Go
  - [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
  - [Effective Go](https://golang.org/doc/effective_go.html)
  - Know and avoid [Go landmines](https://gist.github.com/lavalamp/4bd23295a9f32706a48f)
  - Comment your code.
    - [Go's commenting conventions](http://blog.golang.org/godoc-documenting-go-code)
    - If reviewers ask questions about why the code is the way it is, that's a sign that comments might be helpful.
    - Command-line flags should use dashes, not underscores
    - Naming
      - Please consider package name when selecting an interface name, and avoid redundancy. For example, `storage.Interface` is better than `storage.StorageInterface`.
      - Do not use uppercase characters, underscores, or dashes in package names.
      - Please consider parent directory name when choosing a package name. For example, `pkg/controllers/autoscaler/foo.go` should say `package autoscaler` not `package autoscalercontroller`.
          - Unless there's a good reason, the `package foo` line should match the name of the directory in which the `.go` file exists.
          - Importers can use a different name if they need to disambiguate.
      - Locks should be called `lock` and should never be embedded (always `lock sync.Mutex`). When multiple locks are present, give each lock a distinct name following Go conventions: `stateLock`, `mapLock` etc.
    - [API conventions]
    - [Logging conventions]

## Testing conventions

  - All new packages and most new significant functionality must come with unit tests.
  - Table-driven tests are preferred for testing multiple scenarios/inputs. 
  - Do not expect an asynchronous thing to happen immediately---do not wait for one second and expect a pod to be running. Wait and retry instead.
  - See the [testing guide](testing-guide.md) for additional testing advice.

## Directory and file conventions

  - Avoid package sprawl. Find an appropriate subdirectory for new packages.
    - Libraries with no appropriate home belong in new package subdirectories of `pkg/util`.
  - Avoid general utility packages. Packages called "util" are suspect. Instead, derive a name that describes your desired function. For example, the utility functions dealing with waiting for operations are in the `wait` package and include functionality like `Poll`. The full name is `wait.Poll`.
  - All filenames should be lowercase.
  - Go source files and directories use underscores, not dashes.
    - Package directories should generally avoid using separators as much as possible. When package names are multiple words, they usually should be in nested subdirectories.
  - Document directories and filenames should use dashes rather than underscores.
  - Follow these conventions for third-party code:
    - Go code for normal third-party dependencies is managed using [go modules](https://github.com/golang/go/wiki/Modules).
    - Other third-party code belongs in `third_party`.
      - forked third party Go code goes in `third_party/forked`.
      - forked _golang stdlib_ code goes in `third_party/forked/golang`.
    - Third-party code must include licenses. This includes modified third-party code and excerpts, as well.
