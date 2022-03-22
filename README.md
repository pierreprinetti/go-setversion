# go setversion

I am a version selector for Go.

Assumptions:
* you are running on Linux
* you have Go installed on `/usr/bin/go`
* I can install as `$GOBIN/go` on your system

## Install

Download `go-setversion` and save it as `$GOBIN/go`.

```shell
curl -L https://raw.githubusercontent.com/pierreprinetti/go-setversion/main/go-setversion > "$GOBIN/go" && chmod +x "$GOBIN/go"
```

## Use

Set the current directory to Go v1.18:

```shell
go setversion 1.18
```

Then, operate as usual:

```shell
go build -o myproject .
```

go-setversion will only intercept calls to `go setversion` and will pass the rest to the Go version of your choice.

---

Remove any setversion settings for this directory:

```shell
go setversion
```

## Reset

```shell
rm  ${XDG_CONFIG_HOME:-${HOME}/.config}/go-setversion/paths.conf
```

## Uninstall

```shell
rm -f "$GOBIN/go"
rm -rf ${XDG_CONFIG_HOME:-${HOME}/.config}/go-setversion
```

## Tip

When a new Go version is published, I set it as the default on my system with (for example):

```shell
cd /
go setversion 1.18rc1
```

## How do I work

I save a map of {directory -> Go version} in a config file. Whenever you call `go`, I intercept the call and bounce it to the Go version you have set for `$PWD`.

If the Go version you want is not available on your system, I will install it in `$GOBIN`.
