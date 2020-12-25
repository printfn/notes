# GraphViz (.dot files)

Language reference: https://graphviz.org/doc/info/lang.html

List of attributes: https://graphviz.org/doc/info/attrs.html

Simple example:

```dot
digraph test { a -> {b,c}; b -> c; b -> b; c -> b }
```

![rendered graph](./graphviz/1.png)

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

![rendered graph](./graphviz/2.png)

Using `graph` instead of `digraph`, and `--` instead of `->` creates an undirected graph:

```dot
graph test { a -- b -- c }
```

![rendered graph](./graphviz/3.png)

Edge colors can be changed like this:

```dot
digraph test { a -> b [color=blue] }
```

![rendered graph](./graphviz/4.png)

To change node colors, explicitly declare the node:

```dot
digraph test { a[color=red] a -> b [color=blue] }
```

![rendered graph](./graphviz/5.png)

To create a horizontal graph, add `rankdir=LR` (case-sensitive):

```dot
digraph test { rankdir=LR a->b->c a->c }
```

![rendered graph](./graphviz/6.png)

You can specify directions using `:n` `:ne` `:e` `:se` `:s` `:sw` `:w` `:nw`:

```dot
digraph test { a:e->b:w [taillabel="t"] b->a }
```

![rendered graph](./graphviz/7.png)
