# Package manager

## Platform

DiveScript packages are organized by platform, facilitating the discovery of libraries. A package cannot depend in another package of a different platform.

Here is an example of a manifest:

```toml
[package]
name = "com.q.b"
version = "0.1.0"
# Unreal Engine
platform = "ue"

[dependencies]
"ue:com.author.my_helper" = "1.0.0"
```

It is possible to create a package that does not depend in a platform. In this case, it must omit the `package.platform` property from the manifest and must not depend in platform-tied packages.

## Package name

The name of a package contains dot-delimited names, where the leftmost name is the top domain. Names such as `com.author.library` are preferred, where `com` is the top domain, `author` is a subdomain of `com`, and `library` is a subdomain of `com.author`.

The module path of a package is by default its name, replacing `.` by `::`. For example, a package `com.q.b` is accessed in DiveScript as `com::q::b`, where the crate module is `b`.

```ds
use com::q::b::S;
```

## First-time package

Any user can publish a package without any payment or actual registered domain; however, when a package is published for the first time it must be reviewed by the team to determine if it is legal or has good quality.

The review queue is limited to 5 packages and may take anytime to be reviewed. If a package has been rejected, the user gets a cooldown of 2 days to publish any first-time package again.

## DSDoc

Futurely the package manager should auto generate documentation using Docker containers and host it online.