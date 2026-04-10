# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-10T06:04:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.61K | ± 12.17 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.22K | ± 820.13 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.03K | ± 1.22K | ops/s | 1.1x slower |
| prometheusAdd | 28.55K | ± 67.57 | ops/s | 1.1x slower |
| simpleclientInc | 6.94K | ± 111.10 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.72K | ± 184.50 | ops/s | 4.7x slower |
| simpleclientAdd | 6.64K | ± 92.49 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.42K | ± 26.67 | ops/s | 22x slower |
| openTelemetryAdd | 1.38K | ± 91.65 | ops/s | 23x slower |
| openTelemetryInc | 1.35K | ± 16.78 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 62.45 | ops/s | **fastest** |
| prometheusClassic | 3.05K | ± 201.29 | ops/s | 1.5x slower |
| prometheusNative | 2.28K | ± 132.08 | ops/s | 2.0x slower |
| openTelemetryClassic | 515.22 | ± 15.49 | ops/s | 8.8x slower |
| openTelemetryExponential | 404.58 | ± 9.37 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 347.09K | ± 974.35 | ops/s | **fastest** |
| prometheusWriteToByteArray | 343.47K | ± 1.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 317.54K | ± 781.58 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 314.53K | ± 967.60 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30224.107    ± 820.126  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1384.875     ± 91.655  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.105     ± 16.778  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1419.162     ± 26.672  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28547.637     ± 67.573  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31606.394     ± 12.172  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30028.697   ± 1223.522  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6642.997     ± 92.491  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6942.989    ± 111.100  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6717.690    ± 184.501  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        515.218     ± 15.486  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.584      ± 9.372  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3049.866    ± 201.291  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2279.027    ± 132.081  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4537.119     ± 62.445  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     314525.584    ± 967.598  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     317541.215    ± 781.579  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     343469.191   ± 1212.118  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     347086.945    ± 974.345  ops/s
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
