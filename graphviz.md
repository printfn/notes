# GraphViz (.dot files)

Language reference: https://graphviz.org/doc/info/lang.html

List of attributes: https://graphviz.org/doc/info/attrs.html

Simple example:

```dot
digraph test { a -> {b,c}; b -> c; b -> b; c -> b }
```

You can easily render this by installing `graphviz` and running:

```bash
echo 'digraph test { a -> {b,c}; b -> c; b -> b; c -> b }'|dot -Tpng >out.png
```

Aliases for `kitty`:
```zsh
# in ~/.zshrc
kitty + complete setup zsh | source /dev/stdin
alias icat="kitty icat --align=left"
alias idot="dot -Tpng /dev/stdin -o /dev/stdout|icat"

# then execute
echo 'digraph test { a -> {b,c}; b -> c; b -> b; c -> b }'|icat
```

You can explicitly declare nodes like this:

```dot
digraph test { a; b; c; a -> {b,c}; b -> c; b -> b; c -> b }
```

Semicolons are optional.

`{a,b} -> {c,d}` connects every node in `{a,b}` with every node in `{c,d}`.

Identifiers (for nodes, graphs, etc.) can only contain letters, numbers and
underscores (and not begin with a number), or they must be escaped using `""` or `<>` (HTML escaping).

```dot
digraph test { </> -> <src/> -> "main.rs" }
```

Using `graph` instead of `digraph`, and `--` instead of `->` creates an undirected graph:

```dot
graph test { a -- b -- c }
```

Edge colors can be changed like this:

```dot
digraph test { a -> b [color=blue] }
```

To change node colors, explicitly declare the node:

```dot
digraph test { a[color=red] a -> b [color=blue] }
```

To create a horizontal graph, add `rankdir=LR` (case-sensitive):

```dot
digraph test { rankdir=LR a->b->c a->c }
```

You can specify directions using `:n` `:ne` `:e` `:se` `:s` `:sw` `:w` `:nw`:

```dot
digraph test { a:e->b:w [taillabel="t"] b->a }
```
