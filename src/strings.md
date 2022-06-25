# Strings

When having no spaces

```nushell
hello 
'hello'
"hello"
```

When having spaces

```nushell
'hello world'
"hello world"
```
When having quotes

```nushell
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

```nushell
"Hi\tThere"    # output: Hi   There
'Hi\tThere'    # output: Hi\tThere
```

### String Interpolation

> String interpolation uses `$" "` and `$' '` as ways to wrap interpolated text.

```nushell
let name = "Alice"
$"greetings, ($name)"
```
> By wrapping expressions in (), we can run them to completion and use the results to help build the string.

```nushell
$"2 + 2 is (2 + 2) \(you guessed it!)" 
```
