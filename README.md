# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-04T05:28:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.73K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.90K | ± 283.60 | ops/s | 1.2x slower |
| prometheusAdd | 50.77K | ± 1.30K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.04K | ± 1.84K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 38.45 | ops/s | 9.7x slower |
| simpleclientAdd | 6.56K | ± 9.96 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 210.37 | ops/s | 10x slower |
| openTelemetryInc | 1.43K | ± 86.63 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.23K | ± 124.45 | ops/s | 53x slower |
| openTelemetryAdd | 1.22K | ± 47.17 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 234.19 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 42.99 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 213.79 | ops/s | 1.8x slower |
| openTelemetryClassic | 643.92 | ± 49.56 | ops/s | 8.4x slower |
| openTelemetryExponential | 532.97 | ± 14.88 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.65K | ± 1.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.53K | ± 7.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.17K | ± 8.86K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 512.05K | ± 3.86K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48036.354   ± 1844.076  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1217.007     ± 47.173  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1429.028     ± 86.629  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1231.050    ± 124.447  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50769.722   ± 1296.863  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65731.254   ± 1410.025  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56900.333    ± 283.604  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6560.015      ± 9.963  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6782.028     ± 38.454  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6517.169    ± 210.371  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        643.922     ± 49.560  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.970     ± 14.880  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5418.315    ± 234.193  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3060.401    ± 213.786  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4554.297     ± 42.987  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     512054.853   ± 3864.731  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514174.711   ± 8862.678  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521526.967   ± 7582.100  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533647.417   ± 1964.503  ops/s
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
