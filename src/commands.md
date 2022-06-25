# Commands (Functions)

```nushell
def greet [name] {
  echo "hello " $name "!"
}

greet 'Alice'
```

Valid command names: 

 - `greet` 
 - `get-size`
 - `mycommand123`
 - `mycommand` 
 - `😊`
 - `123`

## Paramters

```nushell
def greet [name: string] {
  echo "hello " $name "!"
}

greet 'Alice'
```
## Optional Types

```nushell
def add [a: int, b: int] {
  echo ($a + $b)
}

add 1 2 

# 3

add 1 '2'

#   × Parse mismatch during operation.
#   ╭─[entry #3:1:1]
# 1 │ add 1 '2'
#   ·       ─┬─
#   ·        ╰── expected int
#   ╰────

```

Accepted types (as of version 0.59.0):

- any
- block
- cell-path
- duration
- path
- expr
- filesize
- glob
- int
- math
- number
- operator
- range
- cond
- bool
- signature
- string
- variable

## Default Values

```nushell
def greet [name = "nushell"] {
  echo "hello " $name | str collect
}

greet 
```
## Optional positional parameters

> By default, positional parameters are required

```nushell
def greet [name: string] {
  echo "hello " $name | str collect
}

greet 

#  × Missing required positional argument.
#   ╭─[entry #2:1:1]
# 1 │ greet
#   ·      ▲
#   ·      ╰── missing name
#   ╰────
#  help: Usage: greet <name>

```
> We can instead mark a positional parameter as optional by putting a `?` after its name

```nushell
def greet [name?: string] {
  echo "hello " $name | str collect
}

greet
```
> When an optional parameter is not passed, its value in the command body is equal to `null` and `$nothing`.

## Sub-Commands

> You can also define subcommands to commands using a space. For example, if we wanted to add a new subcommand to `str`, we can create it by naming our subcommand to start with `str `

```shell
def "str mycommand" [] {
  echo hello
}
```