# Lists

> A list is an ordered collection of values. You can create a list with square brackets, surrounded values separated by spaces and/or commas.

```nushell,noplayground
[foo bar baz] 
[foo, bar, baz]
```
## `update` and `insert`

insert the value 10 into the index 2:

```nushell
[1, 2, 3, 4] | insert 2 10
```
replace the element at index 2 with the value 10:
```nushell
[1, 2, 3, 4] | update 2 10
```
## `prepend` and `append`

>  insert to the beginning of a list or at the end of the list, respectively.

```nushell
[yellow green] | prepend red | append purple
```
## Iterating over list

> use the each command with a block of Nu code that specifies what to do to each item

```nushell
let names = [Mark Tami Amanda Jeremy]
$names | each { |it| $"Hello, ($it)! " }
```
> `--numbered` or `-n` flag can change it to have `index` and `item` values if needed.

```nushell
let names = [Mark Tami Amanda Jeremy]
$names | each -n { |it| $"($it.index + 1) - ($it.item), " }
```

## Filter with `where`

> The `where` command can be used to create a subset of a list, effectively filtering the list based on a condition

```nushell
let colors = [red orange yellow green blue purple]
echo $colors | where ($color | str ends-with 'e')
```
```nushell
let scores = [7 10 8 6 7]
echo $scores | where $it > 7 # [10 8]
```

## Computes a single value with `reduce`

> It uses a block which takes 2 parameters: the current item (conventionally named `it`) and an accumulator (conventionally named `acc`)

>Use `--fold` or `-f` to specify an initial value for the accumulator and `--numbered` or `-n` to use index.

```nushell
let scores = [3 8 4]
echo "total =" ($scores | reduce { |it, acc| $acc + $it }) 
```
```nushell
let scores = [3 8 4]
echo "product =" ($scores | reduce --fold 1 { |it, acc| $acc * $it }) 
```
```nushell
let scores = [3 8 4]
echo $scores | reduce -n { |it, acc| $acc.item + $it.index * $it.item }
```

## Accessing elements

> To access a list item at a given index, use the $name.index form where $name is a variable that holds a list

```nushell
[Mark Tami Amanda Jeremy].2 
```
```nushell
let names = [Mark Tami Amanda Jeremy]
let index = 1
$names | get $index # gives Tami
```

## `in` and `not-in`

> test whether a value is in a list

```nushell
let colors = [red green blue]
'blue' in $colors # true
```
```nushell
5 in [1 2 3] # false
```


## Get size with `length`

```nushell
[red green blue] | length
```

## Check `empty?`

```nushell
let colors = [red green blue]
$colors | empty? # false
```
```nushell
let colors = []
$colors | empty? # true
```

## `any?` and `all?`

> The `any?` command determines if any item in a list matches a given condition

```nushell
[red green blue] | any? ($it | str ends-with "e") # true
```
```nushell
echo [1 10 5] | any? $it > 7 # true
```

> The `all?` command determines if every item in a list matches a given condition. 

```nushell
[red green blue] | all? ($it | str ends-with "e") # false
```
```nushell
echo [2 6 10] | all? $it mod 2 == 0    #true 
```

## To/From list

> The `flatten` command creates a new list from an existing list by adding items in nested lists to the top-level list.

```nushell
echo [1 [2 3] 4 [5 6]] | flatten
# [1 2 3 4 5 6]
```
```nushell
echo [1 [2 3] [4 [5 6]]] | flatten
# [1 2 3 4 [5 6]]
```
```nushell
echo [1 [2 3] [4 [5 6]]] | flatten | flatten
# [1 2 3 4 5 6]
```
> `wrap` command converts a list to a table. Each list value will be converted to a separate row with a single column.

```nushell
echo [red green blue] | wrap 'Colors' 


#  ╭───┬────────╮
#  │ # │ Colors │
#  ├───┼────────┤
#  │ 0 │ red    │
#  │ 1 │ green  │
#  │ 2 │ blue   │
#  ╰───┴────────╯

```