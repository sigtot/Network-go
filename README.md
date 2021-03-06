Network module for Go (UDP broadcast only)
==========================================
[![Go Report Card](https://goreportcard.com/badge/github.com/TTK4145/Network-go)](https://goreportcard.com/report/github.com/TTK4145/Network-go)
[![Go Doc](https://godoc.org/github.com/TTK4145/Network-go?status.svg)](http://godoc.org/github.com/TTK4145/Network-go)


See [`main.go`](main.go) for usage example. The code is runnable with just `go run main.go`


About this fork
---------------

This fork replaces all local imports with package imports from github so that the packages can be imported from other projects.
Example import:
```go
import (
	"github.com/sigtot/Network-go/network/bcast"
	"github.com/sigtot/Network-go/network/localip"
)
```

The packages can then be installed with for example `go get github.com/sigtot/Network-go/network/bcast`.
[dep](https://github.com/golang/dep) should also fetch these automatically and painlessly.

### A small note
The package `connection` was originally named `conn` but was renamed due to a colliding variable name in the implementation,
and to avoid _stealing good names from the user_. From [blog.golang.org/package-names](https://blog.golang.org/package-names):
> Avoid giving a package a name that is commonly used in client code. For example, the buffered I/O package is called bufio, not buf, since buf is a good variable name for a buffer.


Features
--------

Channel-in/channel-out pairs of (almost) any custom or built-in datatype can be supplied to a pair of transmitter/receiver functions. Data sent to the transmitter function is automatically serialized and broadcasted on the specified port. Any messages received on the receiver's port are deserialized (as long as they match any of the receiver's supplied channel datatypes) and sent on the corresponding channel. See [bcast.Transmitter and bcast.Receiver](network/bcast/bcast.go).

Peers on the local network can be detected by supplying your own ID to a transmitter and receiving peer updates (new, current and lost peers) from the receiver. See [peers.Transmitter and peers.Receiver](network/peers/peers.go).

Finding your own local IP address can be done with the [LocalIP](network/localip/localip.go) convenience function, but only when you are connected to the internet.

For Windows users
-----------------

In order to use this module on Windows, you must install a C compiler. I recommend [TDM-GCC](http://tdm-gcc.tdragon.net/download), which is a redistribution of GCC and MinGW.

You may need to add the C toolchain binaries to your Environment Path manually. If you can run `gcc` from either cmd or Powershell, it is already working. If not, open the environment variables dialog the long way, or the short way with `Win+R` and typing `rundll32 sysdm.cpl,EditEnvironmentVariables`. Edit the PATH variable by adding `;C:\TDM-GCC-64\bin` (or whatever your chosen install directory was) at the end of the semi-colon-delimited list. You may also need to restart or log off & back on in order for the changes to take effect. 

The error return values on Windows just display numbers instead of descriptive text. See [here for descriptions of the error codes](https://msdn.microsoft.com/en-us/library/windows/desktop/ms740668(v=vs.85).aspx)

----

If you are wondering why Windows is such a hassle, read the comments in [network/conn/bcast_conn_windows.go](network/conn/bcast_conn_windows.go)






