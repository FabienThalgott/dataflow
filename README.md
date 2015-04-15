# DataFlow

Generate Graphviz documents from a Haskell representation.

## Getting Started

```
cabal install dataflow@0.6.0.0
```

## Usage

![Legend](examples/legend.png)

The following declarations is supported by DataFlow.

<!--- Not Ruby code, but use Ruby code highlighter for .flow code -->

```ruby
boundary 'Title' { ... }
io identifier 'Title'
function identifier 'Title'
database identifier 'Title'
identifier -> identifier 'Operation' 'Data Description'
```

These are used inside a `diagram { ... }`.

## Example

```ruby
diagram 'Webapp' {
  boundary 'Browser' {
    function client 'Client'
  }
  boundary 'Amazon AWS' {
    function server 'Web Server'
    database logs 'Logs'
  }
  io analytics 'Google<br/>Analytics'

  client -> server 'Request /' ''
  server -> logs 'Log' 'User IP'
  server -> client 'Response' 'User Profile'
  client -> analytics 'Log' 'Page Navigation'
}
```

Then generate your output with dot.

```bash
dataflow dfd webapp.flow | dot -Tpng > webapp.png
```

That should generate something like the following.

![Example Output](examples/webapp.png)

## Setup

```bash
cabal sandbox init
cabal install --only-dependencies --enable-tests
cabal configure --enable-tests
```

## Build

```bash
cabal build
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

## Release

```bash
cabal clean && cabal build && cabal sdist &&
```

That outputs a `dist/dataflow-*.tar.gz` that can be distrubuted.
