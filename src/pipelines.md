# Pipelines

```nushell 
["hello" "world"] | str collect "-" | str camel-case
```

## `$in` variable

> The `$in` variable will collect the pipeline into a value for you, allowing you to access the whole stream as a parameter:

```nushell
echo 1 2 3 | $in.1 * $in.2
```
## Multi-line pipelines

> If a pipeline is getting a bit long for one line, you can enclose it within ( and ) to create a subexpression:

```nushell
(
    "01/22/2021" |
    parse "{month}/{day}/{year}" |
    get year
)
```