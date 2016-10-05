ipfs-benchtools
===============
```ipfs-benchtools``` is a collections of scripts for making IPFS benchmarking
easier.

Dependencies
------------

- ```go-ipfs```
- ```rrdtool```
- ```dd```
- ```curl```
- ```jq```
- Optionally ```feh``` if you want to see results automatically.

```ipfs-benchmark``` is required, but it is bundled as a Git submodule.

Commands
--------

```send [--udp] <size in megabytes>``` will create a new temporary IPFS node and host
specified amount of random data for others to get. The optional ```--udp``` switch will
use the UDP/µTP transport instead of TCP. Note the local addresses and the file hash
reference on command output.

```receive [--udp] [--connect <sender address>] <data ref>``` will create a new temporary IPFS
node and download the data specified by the hash reference. It will also collect benchmark
data about the download and finally show a graph. The optional ```--udp`` switch will 
use the UDP/µTP instead of TCP. If applicable you can expliciy specify the address of the
send node by adding ```--connect <sender address>```

The suggested way to do benchmarks is to run ```send``` on one host and
```receive``` on another. Varying network conditions will produce corresponding
results. You can also have both peers on one host to test localhost connection
performance. The commands will create their own IPFS nodes automatically on
different TCP ports.

You can use environment variable ```IPFS_BIN``` to specify ```go-ipfs``` binary
path. This makes testing experimental versions easier.

Example
-------

You can do a simple localhost transfer test using the following steps.

1. ```send 400```
2. Read the data reference hash from the command output.
3. ```receive <hash>``` (on another terminal)
4. Wait for the download to complete.
5. A graph should automatically open, or you can see ```data/ipfs.png```.

This should produce something similar to this:

![localhost 400 MB graph](examples/localhost_400MB.png?raw=true)
