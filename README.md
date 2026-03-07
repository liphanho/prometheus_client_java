# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-07T05:18:26Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.93K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 825.54 | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 317.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.89K | ± 1.13K | ops/s | 1.4x slower |
| simpleclientInc | 6.74K | ± 38.24 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.58K | ± 198.24 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 131.13 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 162.43 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.40K | ± 96.41 | ops/s | 47x slower |
| openTelemetryInc | 1.38K | ± 96.26 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 380.73 | ops/s | **fastest** |
| simpleclient | 4.57K | ± 10.62 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 89.43 | ops/s | 1.8x slower |
| openTelemetryClassic | 661.14 | ± 21.30 | ops/s | 8.0x slower |
| openTelemetryExponential | 552.61 | ± 26.63 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.23K | ± 6.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.79K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.38K | ± 3.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.29K | ± 5.87K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47887.610   ± 1131.967  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1406.183    ± 162.427  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1377.942     ± 96.258  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1404.413     ± 96.406  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51371.971    ± 317.883  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65925.496   ± 1682.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56829.141    ± 825.539  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6232.539    ± 131.127  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6743.413     ± 38.239  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6576.546    ± 198.238  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.137     ± 21.303  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.611     ± 26.627  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5311.693    ± 380.726  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2902.095     ± 89.429  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4572.510     ± 10.616  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521292.679   ± 5867.064  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522379.002   ± 3327.471  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539787.926   ± 4732.048  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548227.419   ± 6812.917  ops/s
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
