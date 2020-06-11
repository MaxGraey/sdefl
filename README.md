# Small Deflate
SDefl is a small bare bone lossless compression library in ANSI C (ISO C90)
that implements the Deflate (RFC 1951) compressed data format specification standard.

SDefl is mainly tuned to get as much speed and compression ratio from as little code
as needed to keep the implementation as concise as possible. In addition since
this library implements the Deflate standard some limitations including a small
match window of only 32kb apply. So don't expect comparable speed or compression
ratio to some of the newer algorithms.

## Features
- Portable single header and source file duo written in ANSI C (ISO C90)
- Small ~300 LoC implementation (Deflate: 170 LoC, Inflate: 150 LoC)
- 8 configurable compression level
- Dual license with either MIT or public domain
- Deflate compiles down to ~3.7 KB uncompressed wasm and ~2.2KB compressed wasm
- Inflate compiles down to ~3.6 KB uncompressed wasm and ~2.2KB compressed wasm

## Usage
For deflating add sdefl(.h+.c) into your project and include `sdefl.h`. To actually
compress memory first call `sdefl_bound` to calculate the maximum number of compressed
output and allocate an compress output memory buffer and pass it along with your
to compress input data and a compression level between `SDEFL_LVL_MIN` and
`SDEFL_LVL_MAX` to the main compression function `sdeflate`.

For inflating add sinfl(.h+.c) into your project and include `sinfl.h`. To
decompress a previously compressed block of memory call `sinflate`. Pass
your compressed block along with its size and an allocated output buffer
with size of the uncompressed block.

## Benchmark
| Compressor name         | Compression| Decompress.| Compr. size | Ratio |
| ---------------         | -----------| -----------| ----------- | ----- |
| libdeflate 1.3 -1       |   147 MB/s |   667 MB/s |    39597378 | 39.60 |
| libdeflate 1.3 -6       |    69 MB/s |   689 MB/s |    36648318 | 36.65 |
| libdeflate 1.3 -9       |    13 MB/s |   672 MB/s |    35197141 | 35.20 |
| libdeflate 1.3 -12      |  8.13 MB/s |   670 MB/s |    35100568 | 35.10 |
| zlib 1.2.11 -1          |    72 MB/s |   307 MB/s |    42298774 | 42.30 |
| zlib 1.2.11 -6          |    24 MB/s |   313 MB/s |    36548921 | 36.55 |
| zlib 1.2.11 -9          |    20 MB/s |   314 MB/s |    36475792 | 36.48 |
| sdefl 1.0 -0            |   115 MB/s |    94 MB/s |    46489930 | 46.49 |
| sdefl 1.0 -1            |   102 MB/s |    96 MB/s |    45291608 | 45.29 |
| sdefl 1.0 -5            |    56 MB/s |   100 MB/s |    43983562 | 43.98 |
| sdefl 1.0 -8            |    45 MB/s |   100 MB/s |    43914863 | 43.91 |
| miniz 1.0 -1            |   122 MB/s |   208 MB/s |    48510028 | 48.51 |
| miniz 1.0 -6            |    27 MB/s |   260 MB/s |    36513697 | 36.51 |
| miniz 1.0 -9            |    23 MB/s |   261 MB/s |    36460101 | 36.46 |


## License
```
------------------------------------------------------------------------------
This software is available under 2 licenses -- choose whichever you prefer.
------------------------------------------------------------------------------
ALTERNATIVE A - MIT License
Copyright (c) 2020 Micha Mettke
Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
------------------------------------------------------------------------------
ALTERNATIVE B - Public Domain (www.unlicense.org)
This is free and unencumbered software released into the public domain.
Anyone is free to copy, modify, publish, use, compile, sell, or distribute this
software, either in source code form or as a compiled binary, for any purpose,
commercial or non-commercial, and by any means.
In jurisdictions that recognize copyright laws, the author or authors of this
software dedicate any and all copyright interest in the software to the public
domain. We make this dedication for the benefit of the public at large and to
the detriment of our heirs and successors. We intend this dedication to be an
overt act of relinquishment in perpetuity of all present and future rights to
this software under copyright law.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
------------------------------------------------------------------------------
```
