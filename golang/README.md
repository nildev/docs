# Go at nildev

This document serves as a best practices and style guide for how to work on new and existing nildev projects written in Go.

## Version

- Wherever possible, use the [latest official release][go-dl] of go

[go-dl]: https://golang.org/dl/

## Style

Go style at nildev essentially just means following the upstream conventions:
  - [Effective Go][effectivego]
  - [CodeReviewComments][codereview]
  - [Godoc][godoc]

It's recommended to set a save hook in your editor of choice that runs `goimports` against your code.

[effectivego]: https://golang.org/doc/effective_go.html
[codereview]: https://github.com/golang/go/wiki/CodeReviewComments
[godoc]: http://blog.golang.org/godoc-documenting-go-code

## Tests

## Dependencies

- Carefully consider adding dependencies to your project: Do you really need it?
- Manage third-party dependencies with [godep][godep-guide]

[godep-guide]: golang/godep.md

## Shared Code

Idiomatic golang generally eschews creating generic utility packages in favour of implementing the necessary code as locally as possible to its use case.
In cases where generic, utility code makes sense, though, move it to `github.com/nildev/lib`.
Use this repository as a first port of call when the need for generic code seems to arise.

## Docker

When creating Docker images from Go projects, use a combination of a `.godir` file and the `golang:onbuild` base image to produce the most simple Dockerfile for a Go project.
The `.godir` file must contain the import path of the package being written (i.e. project's .godir contains "github.com/nildev/project").