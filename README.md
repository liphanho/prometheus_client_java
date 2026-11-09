# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-09T10:33:54Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 26.13K | ± 756.98 | ops/s | **fastest** |
| prometheusNoLabelsInc | 25.80K | ± 30.55 | ops/s | 1.0x slower |
| prometheusInc | 25.67K | ± 75.30 | ops/s | 1.0x slower |
| prometheusAdd | 24.95K | ± 69.66 | ops/s | 1.0x slower |
| simpleclientInc | 6.31K | ± 67.77 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.26K | ± 92.05 | ops/s | 4.2x slower |
| simpleclientAdd | 6.25K | ± 49.87 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 1.08K | ± 78.52 | ops/s | 24x slower |
| openTelemetryInc | 1.04K | ± 65.30 | ops/s | 25x slower |
| openTelemetryAdd | 1.01K | ± 12.75 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.09K | ± 40.27 | ops/s | **fastest** |
| prometheusClassic | 2.40K | ± 152.26 | ops/s | 1.7x slower |
| prometheusNative | 2.00K | ± 100.02 | ops/s | 2.0x slower |
| openTelemetryClassic | 424.87 | ± 28.66 | ops/s | 9.6x slower |
| openTelemetryExponential | 334.91 | ± 8.72 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 297.27K | ± 1.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 294.61K | ± 1.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 278.72K | ± 1.69K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 278.04K | ± 1.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26126.136    ± 756.982  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1008.673     ± 12.746  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1036.780     ± 65.302  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1078.373     ± 78.522  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      24945.170     ± 69.663  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      25666.721     ± 75.296  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      25804.882     ± 30.553  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6248.472     ± 49.874  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6311.016     ± 67.775  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6261.871     ± 92.046  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        424.871     ± 28.658  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        334.906      ± 8.716  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2399.434    ± 152.259  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1999.742    ± 100.024  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4085.041     ± 40.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     278043.492   ± 1318.159  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     278724.927   ± 1685.611  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     294608.912   ± 1395.197  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     297268.823   ± 1824.048  ops/s
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
