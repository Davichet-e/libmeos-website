---
title: "Analyze a trajectory"
date: 2024-08-21T13:57:17+02:00
draft: false
---

MEOS provides more than 300 functions to calculate information of a trajectory, some highlighted ones are:
- Calculate the time weighted centroid:
{{< tabs "CODE-Time-weighted average" >}}
{{< tab "C" >}}
```c
Temporal *tpoint = ...;
GSERIALIZED *centroid = tpoint_twcentroid(tpoint);
```
{{< /tab >}}
{{< tab "Python" >}}
```python
tpoint: TGeomPoint = ...
centroid: shapely.Point = tpoint.time_weighted_centroid()
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
let tpoint: TGeomPoint = /* ... */;
let centroid: geos::Geometry = tpoint.time_weighted_centroid();
```
{{< /tab >}}
{{< /tabs >}}

- Speed
{{< tabs "CODE-Speed" >}}
{{< tab "C" >}}
```c
Temporal *tpoint = ...;
Temporal *speed = tpoint_speed(tpoint);
```
{{< /tab >}}
{{< tab "Python" >}}
```python
tpoint: TGeomPoint = ...
centroid: TFloat = tpoint.speed()
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
let tpoint: TGeomPoint = /* ... */;
let centroid: TFloat = tpoint.speed();
```
{{< /tab >}}
{{< /tabs >}}

