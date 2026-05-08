# CRandom

A lightweight, header-only C++ wrapper around the standard `<random>` library.  
Drop in one file and get clean, straightforward random number generation for `double`, `float`, `uint64_t`, and `int`.

## Installation

Copy `CRandom.hpp` into your project and include it:

```cpp
#include "CRandom.hpp"
```

No build step. No dependencies beyond the C++ standard library.

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

The seed is a full 64-bit value built from two `random_device` draws, feeding a `std::mt19937_64` generator.

### Generating Numbers

Every type supports two overloads — one that uses the stored range, and one that takes an inline range:

```cpp
// Using stored range (see Range section below)
double   d = rng.Double();
float    f = rng.Float();
uint64_t u = rng.uInt64();
int      i = rng.Int();

// Inline range (does not affect stored range)
double   d = rng.Double(0.0, 1.0);
float    f = rng.Float(0.0f, 100.0f);
uint64_t u = rng.uInt64(0, 1000);
int      i = rng.Int(1, 6);
```

### Setting & Resetting Ranges

Set a persistent range so repeated calls don't need to specify bounds every time:

```cpp
rng.SetRangeDouble(0.0, 100.0);
rng.SetRangeFloat(0.0f, 1.0f);
rng.SetRangeUInt64(0, 1000);
rng.SetRangeInt(1, 6);

rng.Double(); // now always draws from [0.0, 100.0]
rng.Int();    // now always draws from [1, 6]

rng.ResetRanges(); // restore all ranges to their defaults
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
- Standard library `<random>` (included in all major compilers)

## License

MIT — see [LICENSE](LICENSE)
