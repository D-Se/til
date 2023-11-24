![3d plot of Yager norm](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExeGdwNHZocm1id3R5Mnc3Nmh6OXJ6d2Uycjl2bmwzYTJtdDY1YjlidiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/uNaVDNfp08LGEWFJRq/giphy.gif)

To create intuitive understanding of something, matrices are cool, plots are cooler and [@animate] are coolerer. If both Lidar (x) and Camera (y) detect an object in foggy weather, wich instrument should a self-driving car trust? No clue! But modulating a lambda for a t-norm (AND in fuzzy logic), we see how we place nuance on instrument impact, to say, adjust for regression in Lidar performance in foggy weather.

```
using Plots
yager_t(λ) = (x, y) -> max(0, 1 - ((1-x)^λ + (1-y)^λ)^(1/λ))
@userplot TPlot
@recipe function f(tp::TPlot)
    λ = first(tp.args)
    yt = yager_t(λ)
    x_vals, y_vals = 0:0.01:1, 0:0.01:1
    t_norm_vals = [yt(x, y) for x in x_vals, y in y_vals]
    title --> "Yager T-Norm (λ = $λ)"
    xlabel --> "x"
    ylabel --> "y"
    zlabel --> "membership"
    camera --> (45, 30)
    seriestype --> :surface # magic!
    x_vals, y_vals, t_norm_vals
end
anim = @animate for λ ∈ 0.1:0.1:1
    surface(tplot(λ))
end
gif(anim, "yager_fps15.gif", fps = 1)
```

[@animate]: https://docs.juliaplots.org/latest/animations/
[Lidar]: https://www.mdpi.com/1424-8220/23/6/2972