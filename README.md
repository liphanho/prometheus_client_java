# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-20T11:01:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.73K | ± 617.62 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.90K | ± 423.37 | ops/s | 1.2x slower |
| prometheusAdd | 62.76K | ± 278.03 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.67K | ± 215.96 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 7.89K | ± 38.31 | ops/s | 9.7x slower |
| simpleclientInc | 7.85K | ± 118.08 | ops/s | 9.8x slower |
| simpleclientAdd | 7.66K | ± 277.71 | ops/s | 10x slower |
| openTelemetryInc | 1.81K | ± 83.33 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.76K | ± 21.83 | ops/s | 44x slower |
| openTelemetryAdd | 1.73K | ± 31.79 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.07K | ± 48.85 | ops/s | **fastest** |
| simpleclient | 5.81K | ± 180.66 | ops/s | 1.2x slower |
| prometheusNative | 3.93K | ± 70.41 | ops/s | 1.8x slower |
| openTelemetryClassic | 779.88 | ± 27.64 | ops/s | 9.1x slower |
| openTelemetryExponential | 687.82 | ± 34.07 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 725.43K | ± 6.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 713.53K | ± 7.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 672.32K | ± 4.62K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 659.01K | ± 12.67K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56670.964    ± 215.962  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1734.018     ± 31.791  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1809.337     ± 83.328  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1756.083     ± 21.830  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62759.879    ± 278.027  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76731.514    ± 617.625  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65904.382    ± 423.370  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7662.208    ± 277.706  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7845.304    ± 118.082  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7890.285     ± 38.311  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        779.881     ± 27.637  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        687.824     ± 34.075  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7068.967     ± 48.855  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3925.709     ± 70.413  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5807.844    ± 180.661  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     659013.548  ± 12671.351  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     672324.190   ± 4623.915  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     713526.722   ± 7915.268  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     725434.684   ± 6872.423  ops/s
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
