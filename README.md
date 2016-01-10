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

```send <size in megabytes>``` will create a new temporary IPFS node and host
specified amount of random data for others to get. Note the file hash reference
on command output.

```receive <data ref>``` will create a new temporary IPFS node and download the
data specified by the hash reference. It will also collect benchmark data about
the download and finally show a graph.

The suggested way to do benchmarks is to run ```send``` on one host and
```receive``` on another. Varying network conditions will produce corresponding
results. You can also have both peers on one host to test localhost connection
performance. The commands will create their own IPFS nodes automatically on
different TCP ports.

You can use environment variable ```IPFS_BIN``` to specify ```go-ipfs``` binary
path. This makes testing experimental versions easier.
