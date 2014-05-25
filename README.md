Peaque
======

Peaque is an unstable priority queue implemented in Lua using binary heaps.

## Installation
Peaque can be installed as a submodule by using the following:
    
    git submodule add git://github.com/FourierTransformer/Peaque.git

This allows for some fancy features. Check out git submodules: http://git-scm.com/book/en/Git-Tools-Submodules. You can then use the require function: `local Peaque = require('Peaque/Peaque')`

or you can also just clone this repo and copy `Peaque.lua` out manually:

    git clone git://github.com/FourierTransformer/Peaque.git

After which you can just use lua's require function: `local Peaque = require('Peaque')`

## Usage
Creating a new priority Queue:
>```lua
local Peaque = require('Peaque')
local q = Peaque:new()
```

Adding some elements. If no weight is given, a weight of `math.huge` is used:
>```lua
-- add some values to the heap
print("Pushing some values...")
q:push("A", 10)
q:push("B", 5)
q:push("C") -- this will have a weight of math.huge applied
q:push("D") -- and so will this
q:push("E") -- and this!
```

Getting the size and checking to see if it's empty:
>```lua
-- Check to see if it's empty
print("Is the queue empty?: ", q:isEmpty()) -- of course not we just pushed!
-- Get the size
print("How many elements in the queue: ", q:size()) -- should be 5
```

Peeking (just take a look at) an popping (actually removing) elements:
>```lua
-- Peek at the top of the queue
print("What's on top?: ", q:peek()) -- should be "B"
-- POP POP!
print("POP:", q:pop()) -- will return "B"
print("POP:", q:pop()) -- will return "A"
print("POP:", q:pop()) -- could return "C", "D", or "E" as the algorithm is unstable.
```

## Algorithm Notes
Peaque uses a binary heap as it's underlying structure. As such the operations have the following runtime properties:

|        | Average | Worst    |
| ------ | ------- | -------- |
| push   | O(1)    | O(log n) |
| pop    | O(n)    | O(log n) |
| peek   | O(1)    | O(1)     |
| isEmpty| O(1)    | O(1)     |
| size   | O(1)    | O(1)     |

and it has a space complexity of O(n).

It's also worth noting that the algorithm is considered "unstable" as elements with the same weight will not be popped off in the order they are pushed on. See the code example on popping under [Usage](#usage)
