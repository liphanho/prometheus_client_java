# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-11T10:12:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.40K | ± 58.90 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.10K | ± 270.54 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.33K | ± 651.17 | ops/s | 1.1x slower |
| prometheusAdd | 28.40K | ± 102.81 | ops/s | 1.1x slower |
| simpleclientInc | 6.67K | ± 109.53 | ops/s | 4.7x slower |
| simpleclientAdd | 6.04K | ± 167.38 | ops/s | 5.2x slower |
| simpleclientNoLabelsInc | 6.02K | ± 392.76 | ops/s | 5.2x slower |
| openTelemetryIncNoLabels | 1.36K | ± 38.29 | ops/s | 23x slower |
| openTelemetryInc | 1.27K | ± 63.96 | ops/s | 25x slower |
| openTelemetryAdd | 1.22K | ± 33.67 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.04K | ± 139.28 | ops/s | **fastest** |
| prometheusClassic | 3.13K | ± 85.20 | ops/s | 1.3x slower |
| prometheusNative | 2.23K | ± 100.62 | ops/s | 1.8x slower |
| openTelemetryClassic | 504.69 | ± 15.74 | ops/s | 8.0x slower |
| openTelemetryExponential | 399.65 | ± 11.59 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.58K | ± 3.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 312.35K | ± 7.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.56K | ± 4.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.90K | ± 4.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29331.128    ± 651.172  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1219.142     ± 33.674  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1273.604     ± 63.962  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1362.007     ± 38.292  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28396.252    ± 102.808  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31402.419     ± 58.896  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31101.559    ± 270.541  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6035.798    ± 167.381  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6672.443    ± 109.528  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6024.567    ± 392.761  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        504.692     ± 15.740  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        399.652     ± 11.585  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3132.296     ± 85.201  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2227.260    ± 100.624  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4040.712    ± 139.283  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294896.083   ± 4517.672  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296558.169   ± 4746.582  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     312347.458   ± 7092.372  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317578.516   ± 3394.223  ops/s
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
