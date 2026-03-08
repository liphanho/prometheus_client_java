# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-08T05:28:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.95K | ± 291.38 | ops/s | 1.1x slower |
| prometheusAdd | 51.80K | ± 62.11 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.17K | ± 870.40 | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 22.76 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.58K | ± 109.73 | ops/s | 10.0x slower |
| simpleclientAdd | 6.10K | ± 143.37 | ops/s | 11x slower |
| openTelemetryAdd | 1.53K | ± 268.06 | ops/s | 43x slower |
| openTelemetryInc | 1.27K | ± 4.40 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.16K | ± 99.67 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.63K | ± 177.57 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 128.20 | ops/s | 1.3x slower |
| prometheusNative | 3.21K | ± 37.48 | ops/s | 1.8x slower |
| openTelemetryClassic | 715.55 | ± 68.84 | ops/s | 7.9x slower |
| openTelemetryExponential | 563.77 | ± 39.60 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 522.13K | ± 11.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.80K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 504.74K | ± 4.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 494.53K | ± 3.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47165.613    ± 870.396  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1528.695    ± 268.059  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1270.044      ± 4.404  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1158.276     ± 99.668  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51801.243     ± 62.108  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65476.927   ± 1313.933  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56952.415    ± 291.381  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6103.688    ± 143.367  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6784.597     ± 22.762  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6578.599    ± 109.732  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.548     ± 68.842  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.768     ± 39.598  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5632.588    ± 177.567  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3211.552     ± 37.480  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4450.038    ± 128.197  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     494525.944   ± 3572.867  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504737.224   ± 4277.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512801.493   ± 5008.932  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     522125.080  ± 11713.208  ops/s
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
