---
title: "Temporal Point"
date: 2024-08-21T13:57:17+02:00
draft: false
---
The central datatype of MEOS is the Temporal Point (`TPoint`), which represents a 2/3D point moving in a spatio-temporal manner.

You can create a `TPoint` from a string:
{{< tabs "CODE-Read a point" >}}
{{< tab "C" >}}
```c
Temporal *tpoint =
    tgeompoint_in("[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03]");
```
{{< /tab >}}
{{< tab "Python" >}}
```python
tpoint = TGeomPoint("[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03]")
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
let tpoint: TGeomPoint =
    "[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03]"
        .parse()
        .unwrap();
```
{{< /tab >}}
{{< /tabs >}}
