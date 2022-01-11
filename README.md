# RewriteTools

[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://peterahrens.github.io/RewriteTools.jl/stable)
[![Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://peterahrens.github.io/RewriteTools.jl/dev)
[![Build Status](https://github.com/peterahrens/RewriteTools.jl/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/peterahrens/RewriteTools.jl/actions/workflows/ci.yml?query=branch%3Amaster)
[![Coverage](https://codecov.io/gh/peterahrens/RewriteTools.jl/branch/master/graph/badge.svg)](https://codecov.io/gh/peterahrens/RewriteTools.jl)
SymbolicUtils.jl provides various utilities for symbolic computing. SymbolicUtils.jl is what one would use to build
a Computer Algebra System (CAS). If you're looking for a complete CAS, similar to SymPy or Mathematica, see
[Symbolics.jl](https://github.com/JuliaSymbolics/Symbolics.jl). If you want to build a crazy CAS for your weird
Octonian algebras, you've come to the right place.

[Symbols in SymbolicUtils](https://symbolicutils.juliasymbolics.org/#creating_symbolic_expressions) carry type information. Operations on them propagate this information. [A rule-based rewriting language](https://symbolicutils.juliasymbolics.org/rewrite/#rule-based_rewriting) can be used to find subexpressions that satisfy arbitrary conditions and apply arbitrary transformations on the matches. The library also contains a set of useful [simplification](https://juliasymbolics.github.io/SymbolicUtils.jl/#simplification) rules for expressions of numeric symbols and numbers. These can be remixed and extended for special purposes.


If you are a Julia package develper in need of a rule rewriting system for your own types, have a look at the [interfacing guide](https://symbolicutils.juliasymbolics.org/interface/).

[**Go to the manual**](https://juliasymbolics.github.io/SymbolicUtils.jl/)

SymbolicUtils.jl is on the general registry and can be added the usual way:
```julia
pkg> add SymbolicUtils
```
or
```julia
julia> using Pkg; Pkg.add("SymbolicUtils")
```

### "I don't want to read your manual, just show me some cool code"
```julia
julia> using SymbolicUtils

julia> SymbolicUtils.show_simplified[] = true

julia> @syms x::Real y::Real z::Complex f(::Number)::Real
(x, y, z, f(::Number)::Real)

julia> 2x^2 - y + x^2
(3 * (x ^ 2)) + (-1 * y)

julia> f(sin(x)^2 + cos(x)^2) + z
f(1) + z

julia> r = @rule sinh(im * ~x) => sin(~x)
sinh(im * ~x) => sin(~x)

julia> r(sinh(im * y))
sin(y)

julia> simplify(cos(y)^2 + sinh(im*y)^2, RuleSet([r]))
1
```

# Citations

- The pattern matcher is an adaption of the one by Gerald Jay Sussman (as seen in [6.945](https://groups.csail.mit.edu/mac/users/gjs/6.945/) at MIT), his use of symbolic programming in the book [SICM](https://groups.csail.mit.edu/mac/users/gjs/6946/sicm-html/book.html) inspired this package.
- [Rewrite.jl](https://github.com/HarrisonGrodin/Rewrite.jl) and [Simplify.jl](https://github.com/HarrisonGrodin/Simplify.jl) by [Harrison Grodin](https://github.com/HarrisonGrodin) also inspired this package.