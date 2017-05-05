Title: aah Application Binary
Desc: Learn about aah application binary internal, run flags, OS signals, cross compile build and artifact naming convention.
Keywords: aah binary, aah app binary, flgas, os signals, cross compile, artifact, artifact naming
---
# Learn About aah Application Binary

Page describe the aah application binary details.

## Table of Contents

  * [Flags](#flags)
  * [Start/Stop script](#start-stop-script)
  * [OS Signals](#os-signals)
  * [Cross Compile Build](#cross-compile-build)
  * [Build Artifact Naming Convention](#build-artifact-naming-convention)

## Flags

Application binary supports following flags.

  * `-version` - display the binary name, version and build date.
  * `-config` - absolute path of external configuration file, gets merge into application before initialize.
  * `-profile` - environment profile name to activate. e.g: dev, qa, prod.

### version

Let's say application binary name is `aahwebsite`. Also build information is available via `aah.AppBuildInfo()` method at runtime.

```bash
aahwebsite -version

# output
Binary Name : aahwebsite
Version     : 381eaa8
Build Date  : 2017-04-25T21:00:45-07:00
```

### config

Supplying external configuration file.

```bash
aahwebsite -config=/etc/aahwebsite/site.conf
```

### profile

Environment profile name to active.

```bash
aahwebsite -profile=qa
```

## Start/Stop script

aah build artifact contains two startup scripts named `aah` and `aah.cmd` for `*NIX` and `Windows`. However you can create your own startup scripts as per your need with supported [flags](#flags).

  * `*NIX` script supports `{start|stop|restart|version}`
  * `Windows` script supports `{start|stop|version}`

Note: `start` command accepts profile and config arguments.

```bash
# Just a sample of `aah` *NIX start script with arguments.
./aahwebsite start qa
./aahwebsite start qa /Users/jeeva/external-config.conf
```

## OS Signals

aah application binary listens to `SIGINT` and `SIGTERM` OS signal and then performs the graceful shutdown with timeout of config value `server.timeout.grace_shutdown` from `aah.conf`.

## Cross Compile Build

Since `go1.5` we can build cross platform build easily. aah framework supports it, refer [Cross Compile Build](aah-cli-tool.html#cross-compile-build)

## Build Artifact Naming Convention

aah build produces the build artifact name as `<app-binary-name>-<version>-<goos>-<goarch>.zip`.

For e.g.: `aahwebsite-381eaa8-darwin-amd64.zip`