# HyperFind

HyperFind is a client application for performing non-indexed search on images on an [OpenDiamond](http://diamond.cs.cmu.edu/) system.


## Pre-requisites
Install `opendiamond.jar`.

Download necessary jar libraries into the `lib/` folder by running:

```bash
(cd lib ; ./get-lib.sh)
```

## Compiling
Install `jdk` and `ant`.
```bash
ant jar
```

## Preconditions for running

HyperFind looks for certain files under `$HOME/.diamond/`.

+ `$HOME/.diamond/NEWSCOPE`: a [ScopeCookie](https://github.com/cmusatyalab/opendiamond/wiki/ScopeCookie) typically 
generated by a scope server.

+ `$HOME/.diamond/codecs/*.codec`: HyperFind looks for codecs here.

+ `$HOME/.diamond/predicates/*.pred`: HyperFind looks for predicates here.

+ `$HOME/.diamond/filters/*`: HyperFind looks for filters referenced in codecs or predicates here.

Typically, codecs/predicates/filters come in a bundle developed separately.

*For definitions of `codec`, `predicate` and `filter`, see https://github.com/cmusatyalab/opendiamond/wiki/StructureOfDiamond .*

## Running

```bash
./hyperfind.sh
```

## Tips

### Viewing ScopeCookie
The ScopeCookie is a base64-encoded string containing the authorized search servers, data sources and expiration time.
You can view the decoded information by
```bash
cat $HOME/.diamond/NEWSCOPE | grep -v \- | base64 -d
```

### Auto placing ScopeCookie (Linux Only)
Installing OpenDiamond on your computer will also install a system hook that automatically renames and places
the ScopeCookie properly when you double-click the downloaded file from the browser.

### Obtaining filters
The common type of downloadable filters (short for saying codecs/predicates/filters) is
a tar ball containing the directories `codec/`, `predicate/` and `filter/`.
Decompress the tar ball and place files under `$HOME/.diamond/` as mentioned above.

### Running HyperFind remotely with X11 forwarding
It has been successful to run HyperFind in a Linux host and forward the GUI to Windows/MacOS.
To do so, you should enable X11 forwarding in your SSH connection and install a X11 server on your OS
(e.g., Xming on Windows, Xquartz on MacOS).