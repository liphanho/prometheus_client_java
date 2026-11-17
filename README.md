# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-17T11:33:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.48K | ± 28.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.36K | ± 1.03K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.62K | ± 1.24K | ops/s | 1.1x slower |
| prometheusAdd | 28.26K | ± 58.85 | ops/s | 1.1x slower |
| simpleclientInc | 6.53K | ± 144.52 | ops/s | 4.8x slower |
| simpleclientAdd | 5.97K | ± 211.70 | ops/s | 5.3x slower |
| simpleclientNoLabelsInc | 5.95K | ± 119.90 | ops/s | 5.3x slower |
| openTelemetryInc | 1.30K | ± 23.81 | ops/s | 24x slower |
| openTelemetryIncNoLabels | 1.26K | ± 109.64 | ops/s | 25x slower |
| openTelemetryAdd | 1.15K | ± 91.54 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.17K | ± 29.95 | ops/s | **fastest** |
| prometheusClassic | 2.99K | ± 73.62 | ops/s | 1.4x slower |
| prometheusNative | 2.00K | ± 76.22 | ops/s | 2.1x slower |
| openTelemetryClassic | 479.12 | ± 10.14 | ops/s | 8.7x slower |
| openTelemetryExponential | 376.18 | ± 11.28 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.55K | ± 2.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 326.50K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 303.52K | ± 1.53K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 296.80K | ± 1.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29619.207   ± 1242.105  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1149.020     ± 91.544  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1297.582     ± 23.814  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1258.610    ± 109.644  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28258.131     ± 58.846  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31483.535     ± 28.539  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30356.174   ± 1031.494  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5973.976    ± 211.696  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.638    ± 144.518  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5945.559    ± 119.896  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        479.117     ± 10.135  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        376.181     ± 11.284  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2986.610     ± 73.619  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1997.118     ± 76.215  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4166.925     ± 29.952  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     296802.352   ± 1147.948  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     303515.066   ± 1527.689  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     326498.197   ± 2770.045  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327546.408   ± 2306.500  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
