```
__  __        ___                          _    _ _ 
\ \/ / /\ /\ / _ \__ _ ___ _____      ____| |  (_) |
 \  / / //_// /_)/ _` / __/ __\ \ /\ / / _` |  | | |
 /  \/ __ \/ ___/ (_| \__ \__ \\ V  V / (_| |_ | | |
/_/\_\/  \/\/    \__,_|___/___/ \_/\_/ \__,_(_)/ |_|
                                             |__/   
```
[![Build Status](https://travis-ci.org/freeboson/XKPasswd.jl.svg?branch=master)](https://travis-ci.org/freeboson/XKPasswd.jl)
[![Coverage Status](https://coveralls.io/repos/freeboson/XKPasswd.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/freeboson/XKPasswd.jl?branch=master)
[![codecov.io](http://codecov.io/github/freeboson/XKPasswd.jl/coverage.svg?branch=master)](http://codecov.io/github/freeboson/XKPasswd.jl?branch=master)


This is a password generator written in [Julia](https://julialang.org), inspired
by [XKCD #963](https://xkcd.com/936/). There are word lists bundled with this
repo, including the lists from [this
repository](https://github.com/first20hours/google-10000-english) (included as
a git submodule), but you can use also use your own.

Quickstart
----------

Running this is trivial why Julia's package manager:

```jlcon
julia> Pkg.add("XKPasswd")
INFO: Cloning cache of XKPasswd from https://github.com/freeboson/XKPasswd.jl.git
INFO: Installing XKPasswd v0.0.1

julia> using XKPasswd;

julia> XKPasswd.generate(4, append_digit=false) # output here is just a joke
Estimated entropy: ~45 bits.
1-element Array{String,1}:
 "correct horse battery staple"

julia> XKPasswd.generate(6, npws=5, delimstr="-", capitalize=true)
Estimated entropy: ~70 bits.
5-element Array{String,1}:
 "Succeed-Ruin-Variety-Rice-Claim-Be-1"
 "City-Ask-Right-Arrow-Excite-Disregard-9"
 "Uncle-Stem-Harbor-Fool-Give-Breathe-4"
 "Borrow-Importance-Descendant-Height-Service-Sow-7"
 "Below-Union-Envelope-Back-Asleep-First-1"
```

Don't use any of the above as your own password :)

Word lists
----------

The word lists provided by `XKPasswd.jl` are stored in `data/`, but you can
access them in `XKPasswd.generate` from the `WordList` enum. The options are:

+ `XKPasswd.simple`, a list of 2248 simple words
+ `XKPasswd.jargon`, a list of 9460 more complicated words
+ `XKPasswd.google_20k`, a list of 20k words with *UK spelling*
+ `XKPasswd.google_10k`, a list of 10k words with *UK spelling*
+ `XKPasswd.google_10k_clean`, (86 "bad" words removed) with *UK spelling*
+ `XKPasswd.google_10k_usa` the 10k list with *USA spelling*
+ `XKPasswd.google_10k_usa_clean` (98 "bad words removed)
+ `XKPasswd.google_10k_usa_clean_short` 2186 words with length < 5
+ `XKPasswd.google_10k_usa_clean_medium` 5471 words with length in [5,8]
+ `XKPasswd.google_10k_usa_clean_long` 2246 words with length > 8

All of the lists specified by `XKPasswd.google_*` are derived from [Google's
Trillion Word Corpus](https://books.google.com/ngrams/info). See [this
repository](https://github.com/first20hours/google-10000-english) for more
details. Alternatively, you can pass `XKPasswd.generate` a `String` with the
path to your favorite word list.

Examples
--------

```julia
using XKPasswd;

XKPasswd.generate(4, XKPasswd.jargon, npws=10)
XKPasswd.generate(6, XKPasswd.google_10k_usa_clean, delimstr="-",
                  capitalize=true)
XKPasswd.generate(4, "./some_other_list.txt", npws=5, append_digit=false)
```

The three commands above will all produce `Array{String,1}` instances with:

1. 10 passwords with 4 random words from the `XKPasswd.jargon` builtin word
   list, delimited by spaces, and with a single random digit at the end
2. 1 password with 6 random words from the `XKPasswd.google_10k_usa_clean`
   builtin word list, delimited by hyphens, with the first character of each
   word capitalized, and with a single random digit at the end
3. 5 passwords with 4 random words from the file `some_other_list.txt` in the
   current working directory, delimited by spaces

