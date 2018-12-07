# JSONPatch - Swift 4 json-patch implementation
[![Apache 2 License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Supported Platforms](https://img.shields.io/badge/platform-ios%20%7C%20macos%20%7C%20tvos-lightgrey.svg)](http://developer.apple.com)
[![Build System](https://img.shields.io/badge/build%20system-spm-yellow.svg)](https://swift.org/package-manager/)

JSONPatch is a a swift module implements json-patch [RFC6902](https://tools.ietf.org/html/rfc6902). JSONPatch uses [JSONSerialization](https://developer.apple.com/documentation/foundation/jsonserialization) from Foundation, and has no dependencies on third-party libraries.

The implementation uses the [JSON Patch Tests](https://github.com/json-patch/json-patch-tests) project for unit tests to validate its correctness.

# Release
0.3 - Cocoapods support.

# Usage

## Applying Patches
```swift
import JSONPatch

let sourceData = Data("""
                      {"foo": "bar"}
                      """.utf8)
let patchData = Data("""
                     [{"op": "add", "path": "/baz", "value": "qux"}]
                     """.utf8)

let patch = try! JSONPatch(data: patchData)
let patched = try! patch.apply(to: sourceData)
```

## Generating Patches
```swift
import JSONPatch

let sourceData = Data("""
                      {"foo": "bar"}
                      """.utf8)
let targetData = Data("""
                      {"foo": "bar", "baz": "qux"}
                      """.utf8)
let patch = try! JSONPatch(source: sourceData, target: targetData)
let patchData = try! patch.data()
```

# Installation

## Swift Package Manager
Add JSONPatch as a dependency to your projects Package.swift. For example: -

```swift
// swift-tools-version:4.0
import PackageDescription

let package = Package(
    name: "YourProject",
    dependencies: [
        // Dependencies declare other packages that this package depends on.
        .package(url: "https://github.com/raymccrae/swift-jsonpatch.git", .branch("master"))
    ],
    targets: [
        // Targets are the basic building blocks of a package. A target can define a module or a test suite.
        // Targets can depend on other targets in this package, and on products in packages which this package depends on.
        .target(
            name: "YourProject",
            dependencies: ["JSONPatch"]),
    ]
)
```

# License

Apache License v2.0