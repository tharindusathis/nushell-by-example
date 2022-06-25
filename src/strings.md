# Strings

When having no spaces

```nushell,noplayground
hello 
'hello'
"hello"
```

When having spaces

```nushell,noplayground
'hello world'
"hello world"
```
When having quotes

```nushell,noplayground
'say "hello world"'
"say 'hello world'"
"say \"hello world\""
```
Escape characters

```
\"      - double-quote character
\'      - single-quote character
\\      - backslash
\/      - forward slash
\b      - backspace
\f      - formfeed
\r      - carriage return
\n      - newline (line feed)
\t      - tab
\uXXXX  - a unicode character 
```
> Single-quoted strings don't do anything to the text they're given

```nushell,noplayground
"Hi\tThere"    # output: Hi   There
'Hi\tThere'    # output: Hi\tThere
```

### String Interpolation

> String interpolation uses `$" "` and `$' '` as ways to wrap interpolated text.

```nushell,editable
let name = "Alice"
$"greetings, ($name)"
```
> By wrapping expressions in (), we can run them to completion and use the results to help build the string.

```nushell,editable
$"2 + 2 is (2 + 2)" 
```

```nushell,editable
echo $"6 x 7 = (6 * 7)"
```

## `str` commands
### Change string case

- [camel-case](#str-camel-case)
- [capitalize](#str-capitalize)
- [downcase](#str-downcase)
- [kebab-case](#str-kebab-case)
- [pascal-caes](#str-pascal-caes)
- [screaming-snake-case](#str-screaming-snake-case)
- [snake-case](#str-snake-case)
- [title-case](#str-title-case)
- [upcase](#str-upcase)

#### `str camel-case`

> convert a string to **camelCase**

```nushell
'NuShell' | str camel-case      
```
#### `str capitalize`


```nushell
'good day' | str capitalize  
```
#### `str downcase`

> convert a string to **downcase**

```nushell
'TESTa' | str downcase
```
#### `str kebab-case`

```nushell
'NuShell' | str kebab-case
```

#### `str pascal-caes`

```nushell
'nu-shell' | str pascal-case
```

#### `str screaming-snake-case`
```nushell
"NuShell" | str screaming-snake-case
```

#### `str snake-case`

```nushell
"NuShell" | str snake-case
```
#### `str title-case`

```nushell
"nu-shell" | str title-case
```
#### `str upcase`

```nushell
'nu' | str upcase
```



### Other commands

#### `str collect (seperator)`

>  Concatenate multiple strings into a single string, with an optional separator between each

```nushell
['nu', 'shell'] | str collect
```

Create a string from input with a separator
```nushell
['nu', 'shell', 'is', 'great'] | str collect '-'
```
#### `str contains`

> Checks if string contains pattern

```shell
'my_library.rb' | str contains '.rb'
```
not contain
```shell
'my_library.rb' | str contains --not '.rb'
```

case insensitive
```shell
'my_library.rb' | str contains -i '.RB'
```

in a table
```shell
[[ColA ColB]; [test 100]] | str contains 'e' ColA
```
in a list 
```shell
[one two three] | str contains o
```

#### `str ends-with`

...


## To String

using `into string`
```nushell
123 | into string
```
string interpolation
```nushell
$'(123)
```
`build-string`
```nushell
build-string (123)
```

## Coloring Strings

```nushell
$'(ansi purple_bold)This text is a bold purple!(ansi reset)'
```