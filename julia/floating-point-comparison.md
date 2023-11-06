Comparing floating points is slower than comparing integers, and may be a bottleneck for large scale adoption of many-valued logic.

## Background
I want to implement fuzzy numbers, for which inputs like `Inf`, `-Inf`, `NaN` do not make sense. I have a type with a constructor, which calls `isfinite`, that checks for exactly that.

```julia
using BenchmarkTools
x, y = 1, 1.0
@btime isfinite($x) # 2.206 ns (0 allocations: 0 bytes)
@btime isfinite($y) # 4.383 ns (0 allocations: 0 bytes)
```

Looking at the [source code][float-finite] of `finite`, integers are always finite, thus `isfinite` is hardcoded to `true`.
For floats, `!isnan(x - x)`, which is the same as `x-x ≠ x-x`.

Nanoscale operations are normally not a problem. Yet, for performant fuzzy systems, where some 100k or 1M fuzzy numbers are generated, this may be a performance bottleneck. Implementations on top of floating point numbers are susceptible to this. Alternatives exist, such as [posit numbers], but are not yet mature enough.

[float-finite]: https://github.com/JuliaLang/julia/blob/55b07290c975982fa784e1aa1ccc4aece2a2206d/base/float.jl#L674-L676
[posit numbers]: https://www.superfri.org/index.php/superfri/article/view/137