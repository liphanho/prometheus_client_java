# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-14T07:58:05Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.49K | ± 496.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.17K | ± 604.56 | ops/s | 1.2x slower |
| prometheusAdd | 48.17K | ± 318.19 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.41K | ± 850.98 | ops/s | 1.3x slower |
| simpleclientInc | 6.26K | ± 57.00 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.96K | ± 209.00 | ops/s | 10.0x slower |
| simpleclientAdd | 5.76K | ± 203.75 | ops/s | 10x slower |
| openTelemetryAdd | 1.28K | ± 29.38 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.26K | ± 8.43 | ops/s | 47x slower |
| openTelemetryInc | 1.24K | ± 43.78 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 42.23 | ops/s | **fastest** |
| prometheusClassic | 4.01K | ± 327.41 | ops/s | 1.1x slower |
| prometheusNative | 3.09K | ± 93.47 | ops/s | 1.4x slower |
| openTelemetryClassic | 576.37 | ± 17.40 | ops/s | 7.6x slower |
| openTelemetryExponential | 501.82 | ± 10.19 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.10K | ± 6.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 624.52K | ± 5.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 604.84K | ± 7.66K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 594.40K | ± 7.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44406.427    ± 850.982  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1283.845     ± 29.376  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1241.323     ± 43.777  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1257.413      ± 8.433  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48174.176    ± 318.186  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59494.856    ± 496.692  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51170.360    ± 604.559  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5757.611    ± 203.746  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6264.653     ± 56.996  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5955.207    ± 208.997  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        576.370     ± 17.403  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        501.824     ± 10.194  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4006.653    ± 327.414  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3087.593     ± 93.467  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4366.377     ± 42.226  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     594395.812   ± 7292.993  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     604838.893   ± 7655.381  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     624515.193   ± 5912.054  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643098.409   ± 6279.925  ops/s
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
