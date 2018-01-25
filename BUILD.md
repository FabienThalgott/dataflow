# Build Instructions for Kali Linux as root user

## Prerequisite

```bash
git clone https://github.com/FabienThalgott/dataflow.git
apt-get install -y haskell-platform zlib1g-dev graphviz


ghc-pkg unregister HTTP
ghc-pkg unregister vector
ghc-pkg unregister QuickCheck
ghc-pkg unregister tf-random
```

## Setup + Build + Install

```bash
cabal update
cabal sandbox init
cabal install --only-dependencies
cabal configure
cabal install

ln -s /root/dataflow/.cabal-sandbox/bin/dataflow /usr/bin/dataflow

```

## Generate png from .flow

```bash
 dataflow dfd webapp.flow | dot -Tpng > webapp.png
```

## Tests

```bash
./run-tests.sh
# or...
./watch-tests.sh
```

## Building the Examples

```bash
make -C examples
```
