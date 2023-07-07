# go setversion

I am a version selector for Go.

Assumptions:
* you are running on Linux
* you have Go installed on `/usr/bin/go`
* I can install as `$GOBIN/go` on your system

## Install/Update

Download `go-setversion` and save it as `$GOBIN/go`.

```shell
curl -L https://codeberg.org/pierreprinetti/go-setversion/raw/branch/main/go-setversion > "$GOBIN/go" && chmod +x "$GOBIN/go"
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

go-setversion only intercepts calls to `go setversion` and passes the rest to the Go version of your choice.

---

## Reset

Remove setversion settings for the current directory:

```shell
go setversion
```

Remove setversion settings for the whole system:

```shell
./go-setversion reset
```

or

```shell
rm ${XDG_CONFIG_HOME:-${HOME}/.config}/go-setversion/paths.conf
```

## Uninstall

```shell
rm -f "$GOBIN/go"
rm -rf ${XDG_CONFIG_HOME:-${HOME}/.config}/go-setversion
```

## Tip

When a new Go version is published, set it as the default for your system with (for example):

```shell
cd /
go setversion 1.18rc1
```

## How it works

`go-setversion` saves a map of {directory -> Go version} in a config file. Whenever you call `go`, it intercepts the call and bounces it to the Go version you have set for `$PWD`.

If the Go version you want is not available on your system, it installs it to `$GOBIN`.
