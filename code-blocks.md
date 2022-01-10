---
title: Code Blocks
desc: Short, but powerful, drop-in code segments.
layout: default
resource: true
categories: [Tutorials]
---

{% include header.html %}

# Gaussian Bell Curve
_By Dee Schaedler_
```ruby
def gaussian(mean, stddev)
  theta = 2 * Math::PI * rand
  rho = Math.sqrt(-2 * Math.log(1 - rand))
  scale = stddev * rho
  [mean + scale * Math.cos(theta), mean + scale * Math.sin(theta)]
end

```

# Random Integer in Range
_By Dee Schaedler_
```ruby
def randr(min, max)
  rand(max - min + 1) + min
end

```
