# CRandom

A lightweight, header-only C++ wrapper around the standard `<random>` library.  

Random number generation for `double`, `float`, `uint64_t`, and `int`.

Dependent only on C++ `<random>` library.

## Installation

Copy `CRandom.hpp` into your project and include it:

```cpp
#include "CRandom.hpp"
```

## Quick Start

```cpp
CRandom rng;

// One-off calls using default ranges
int   i = rng.Int();     // [INT_MIN, INT_MAX]
float f = rng.Float();   // [0.0f, 1.0f]

// One-off calls with an inline range
double d = rng.Double(0.0, 100.0);
int    n = rng.Int(1, 6); // roll a die
```

## Usage

### Construction & Seeding

```cpp
CRandom rng;       // seeded automatically via std::random_device
rng.ResetSeed();   // re-seed with a new random_device value
```

### Generating Numbers

```cpp
// Using stored range (see Range section below)
double   d = rng.Double();
float    f = rng.Float();
uint64_t u = rng.uInt64();
int      i = rng.Int();

// Inline range overloads (does not affect stored range) 
double   d = rng.Double(0.0, 1.0);
float    f = rng.Float(0.0f, 100.0f);
uint64_t u = rng.uInt64(0, 1000);
int      i = rng.Int(1, 6);
```

### Setting & Resetting Ranges

SetRange functions save persistent ranges for future use.

Alternative to inline range replacement. Higher preformance.

```cpp
rng.SetRangeDouble(0.0, 100.0);
rng.SetRangeFloat(0.0f, 1.0f);
rng.SetRangeUInt64(0, 1000);
rng.SetRangeInt(1, 6);

rng.Double(); // now always draws from [0.0, 100.0]
rng.Int();    // now always draws from [1, 6]

rng.ResetRanges(); // restore all ranges to their default ranges below
```

**Default ranges:**

| Type       | Default Range                      |
|------------|------------------------------------|
| `double`   | `[0.0, 1.0]`                       |
| `float`    | `[0.0f, 1.0f]`                     |
| `uint64_t` | `[0, 2^64 - 1]`                    |
| `int`      | `[INT_MIN, INT_MAX]`               |

## Requirements

- C++11 or later

## License

MIT — see [LICENSE](LICENSE)
