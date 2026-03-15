# xoshiro256** written in Lua

This repo reimplemented the `xoshiro256**` random generation algorithm in Lua,
which is the algorithm used by `math.random` of original Lua 5.4.

The code is just a "translated version" of [source code of math.random]
(https://github.com/lua/lua/blob/master/lmathlib.c#L274) to get behavior
that exactly same as standard `math.random` and `math.randomseed` function.

## Why do this?

Standard `math.random` doesn't allow us create individual random generators,
since it uses a global random state which stores in its upvalues.

This work presents a random generator constructor with following features:

- You can construct many random generators with their own random states
- Random generation algorithm is totally same as the standard `math.random`

## Usage

```lua
local rand = require "xoshiro256starstar"

-- random state is stored in this variable. And it will be initialized using random seed
local gen = rand()

-- you can reset the seed just like `math.randomseed`
gen:randomseed(1234)

-- And the `random` method is just same as `math.random` too
gen:random(1000) -- generate random number within [1, 1000].

gen = rand(1234) -- you can set seed in the constructor too.
```

## Todos

- I didn't take 32-bit architectures into consideration
- English is not my first language so there could be lots of typo or grammar
mistakes in the code and doc.
