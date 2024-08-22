Welcome to the MEOS Quickstart guide! This guide will help you get started with MEOS, the C library for manipulating temporal and spatiotemporal data. We'll walk through setting up a simple project, creating temporal data, and performing basic operations. Let's dive in!


## 1. Creating a Simple Temporal Point

Let's create a simple temporal point representing a moving object's trajectory over time.

{{< tabs "CODE - Creating a Temporal Point" >}}
{{< tab "C" >}}
```c
#include "meos.h"
#include <stdio.h>

int main() {
    meos_initialize(NULL, NULL);

    // Define a temporal point in WKT format + timestamp
    char *wkt = "POINT(1 1)@2000-01-01";
    Temporal *tpoint = tgeompoint_in(wkt);

    char *out = tgeompoint_out(tpoint);

    printf("%s\n", out);
    
    // Free allocated memory
    free(tpoint); 
    
    meos_finalize();
    return 0;
}
```
{{< /tab >}}
{{< tab "Python" >}}
```python
from pymeos import TGeomPoint, meos_initialize

meos_initialize("UTC")
# Create a temporal point
tpoint = TGeomPoint("POINT(1 1)@2000-01-01")

print(tpoint)
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
use meos::{init, temporal::{TGeomPoint, TFloat}};

fn main() {
    init();
    // Create a temporal point
    let tpoint: TGeomPoint = "POINT(1 1)@2000-01-01".parse().unwrap();

    println!("{:?}", tpoint);
}
```
{{< /tab >}}
{{< /tabs >}}

## 2. Calculating Speed from Temporal Point

Once you have your temporal point, you can easily calculate the speed of the moving object.

{{< tabs "CODE - Calculating Speed" >}}
{{< tab "C" >}}
```c
#include "meos.h"
#include <stdio.h>

int main() {
    meos_initialize(NULL, NULL);

    // Define a temporal point
    char *str = "{[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03], [Point(1 0)@2001-01-04, Point(0 0)@2001-01-05]}";
    Temporal *tpoint = tgeompoint_in(str);
    Temporal *speed = tpoint_speed(tpoint);

    char *out = tfloat_out(tpoint);

    printf("Speed: %s\n", out);
    
    // Free allocated memory
    free(tpoint);
    free(speed);
    
    meos_finalize();
    return 0;
}
```
{{< /tab >}}
{{< tab "Python" >}}
```python
from pymeos import TGeomPoint, meos_initialize

meos_initialize("UTC")
# Create a temporal point
tpoint = TGeomPoint(
    "{[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03], [Point(1 0)@2001-01-04, Point(0 0)@2001-01-05]}"
)
speed: TFloat = tpoint.speed()

print(speed)
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
use meos::{init, temporal::{TGeomPoint, TFloat}};

fn main() {
    init();
    // Create a temporal point
    let tpoint: TGeomPoint = "POINT(1 1)@2000-01-01".parse().unwrap();
    let speed: TFloat = tpoint.speed();

    println!("{:?}", speed);
}
```
{{< /tab >}}
{{< /tabs >}}

## 3. Querying Temporal Data

You can also perform temporal queries, such as finding the location of the object at a specific time.

{{< tabs "CODE - Querying temporal data" >}}
{{< tab "C" >}}
```c
#include "meos.h"
#include <stdio.h>

int main() {
    meos_initialize(NULL, NULL);

    // Define a temporal point
    char *str = "{[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03], [Point(1 0)@2001-01-04, Point(0 0)@2001-01-05]}";
    TimestampZ ts = pg_timestamptz_in("2001-01-03");
    Temporal *tpoint = tgeompoint_in(str);
    Temporal *instant = temporal_at_timestamp(tpoint, ts);

    char *out = tgeompoint_out(instant);

    printf("Point at specific timestamp: %s\n", out);
    
    // Free allocated memory
    free(tpoint);
    free(instant);
    
    meos_finalize();
    return 0;
}
```
{{< /tab >}}
{{< tab "Python" >}}
```python
from pymeos import TGeomPoint, meos_initialize
from datetime import datetime

meos_initialize("UTC")
# Create a temporal point
tpoint = TGeomPoint(
    "{[Point(0 0)@2001-01-01, Point(1 1)@2001-01-02, Point(1 0)@2001-01-03], [Point(1 0)@2001-01-04, Point(0 0)@2001-01-05]}"
)
instant = tpoint.at(datetime(2001, 1, 3))

print(instant)
```
{{< /tab >}}
{{< tab "Rust" >}}
```rust
use meos::{init, temporal::{TGeomPoint, TFloat}};
use chrono::utc;
fn main() {
    init();
    // Create a temporal point
    let tpoint: TGeomPoint = "POINT(1 1)@2000-01-01".parse().unwrap();
    let timestamp = Utc.with_ymd_and_hms(2020, 1, 1, 0, 0, 0).unwrap();
    let instant: TGeomPoint = tpoint.at_timestamp(timestamp);

    println!("{:?}", instant);
}
```
{{< /tab >}}
{{< /tabs >}}

## 4. Wrapping Up

In this quickstart guide, you've learned how to create a temporal point, calculate speed, and query the location of an object at a specific time using MEOS. Explore further by checking out more advanced topics and the full API reference [here](api-reference-link).

If you encounter any issues or have questions, don't hesitate to reach out to the [community](community-link) or consult the [troubleshooting guide](troubleshooting-link).

Happy coding with MEOS!