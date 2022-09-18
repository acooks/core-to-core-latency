Measuring CPU core-to-core latency
==================================

We measure the latency it takes for a CPU to send a message to another CPU via
its cache coherence protocol.

By pinning two threads on two different CPU cores, we can get them to do a bunch
of compare-exchange operation, and measure the latency.

Results
-------

**See the results notebook for stats and graphics: [results/results.ipynb](results/results.ipynb).**

CPU                                                                   | Median Latency
----------------------------------------------------------------------| ----------------
Intel Xeon Platinum 8375C @ 2.90GHz 32 Cores (Ice Lake, 3rd gen)      | 51ns
Intel Xeon Platinum 8275CL @ 3.00GHz 24 Cores (Cascade Lake, 2nd gen) | 47ns
Intel Core i9-9900K @ 3.60 GHz 8 Cores (Coffee Lake, 8th gen)         | 21ns
Intel Xeon E5-2695 v4 @ 2.10GHz 18 Cores (Broadwell, 5th gen)         | 44ns
AMD EPYC 7R13 @ 48 Cores (Milan, 3rd gen)                             | 23ns and 107ns
AWS Graviton3 @ 64 Cores (Arm Neoverse, 3rd gen)                      | 46ns
AWS Graviton2 @ 64 Cores (Arm Neoverse, 2rd gen)                      | 47ns

How to use
----------

```
$ cargo run --release
   Compiling core-to-core-latency v0.1.0 (/Users/pafy/core-to-core-latency)
    Finished release [optimized] target(s) in 0.96s
     Running `target/release/core-to-core-latency`
Num cores: 10
Using RDTSC to measure time: false
Num round trips per samples: 1000
Num samples: 300
Showing latency=round-trip-time/2 in nanoseconds:

       0       1       2       3       4       5       6       7       8       9
  0
  1   52±6
  2   38±6    39±4
  3   39±5    39±6    38±6
  4   34±6    38±4    37±6    36±5
  5   38±5    38±6    38±6    38±6    37±6
  6   38±5    37±6    39±6    36±4    49±6    38±6
  7   36±6    39±5    39±6    37±6    35±6    36±6    38±6
  8   37±5    38±6    35±5    39±5    38±6    38±5    37±6    37±6
  9   48±6    39±6    36±6    39±6    38±6    36±6    41±6    38±6    39±6

Min  latency: 34.5ns ±6.1 cores: (4,0)
Max  latency: 52.1ns ±9.4 cores: (1,0)
Mean latency: 38.4ns
```

License
-------

MIT
