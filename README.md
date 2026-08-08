# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-08T04:42:32Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.14K | ± 164.72 | ops/s | 1.1x slower |
| prometheusAdd | 51.55K | ± 138.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.97K | ± 1.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 64.27 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.41K | ± 61.50 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 170.70 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 300.49 | ops/s | 45x slower |
| openTelemetryInc | 1.28K | ± 38.78 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 78.76 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 159.64 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 32.85 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 31.83 | ops/s | 1.7x slower |
| openTelemetryClassic | 652.03 | ± 19.07 | ops/s | 8.3x slower |
| openTelemetryExponential | 548.01 | ± 37.09 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.20K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 515.89K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.24K | ± 9.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.48K | ± 5.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47970.784   ± 1028.581  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1463.337    ± 300.494  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1279.200     ± 38.775  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1201.660     ± 78.758  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51554.172    ± 138.605  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65329.408   ± 1709.565  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57138.583    ± 164.725  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6325.679    ± 170.703  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6657.449     ± 64.274  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6409.876     ± 61.495  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.029     ± 19.074  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.011     ± 37.089  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5387.919    ± 159.644  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3159.846     ± 31.825  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4456.727     ± 32.847  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495479.796   ± 5550.280  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505241.540   ± 9246.036  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515888.934   ± 4732.609  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526201.411   ± 3633.715  ops/s
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
