I came across [SymbolicRegression] at [JuliaCon] that uses binary trees and loop vectorization to efficiently fuse operations such as `cos(+(x, y))`.

This approach may be applicable to fuzzy systems, where an arbitary number of fuzzy rules contain `&, |, !, -->` binary and unary functions. Generating rule bases and pruning these, is as of yet, rather tough.

```
# pseudo code for a fuzzy rule
@rule cheap tip = horrible food | poor quality & bad service

# under the hood, leafs nodes can be made for
|(food[:horrible], &(quality[:poor], service[:bad]))
```

1. fuzzy rule interface can render high performance computing within reach of domain experts. 
2. symbolic representation of operators can render high performance computing viable for fuzzy library developers.

[SymbolicRegression]: https://github.com/MilesCranmer/SymbolicRegression.jl
[JuliaCon]: https://www.youtube.com/watch?v=QLiQJDNwt4o