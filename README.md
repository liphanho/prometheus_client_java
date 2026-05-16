# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-16T06:44:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.59K | ± 615.64 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.96K | ± 896.39 | ops/s | 1.2x slower |
| prometheusAdd | 47.89K | ± 280.78 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.28K | ± 830.14 | ops/s | 1.3x slower |
| simpleclientInc | 6.25K | ± 128.35 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.13K | ± 194.65 | ops/s | 9.7x slower |
| simpleclientAdd | 5.85K | ± 236.74 | ops/s | 10x slower |
| openTelemetryInc | 1.33K | ± 92.50 | ops/s | 45x slower |
| openTelemetryAdd | 1.32K | ± 92.16 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 9.49 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.60K | ± 44.67 | ops/s | **fastest** |
| prometheusClassic | 4.20K | ± 317.01 | ops/s | 1.1x slower |
| prometheusNative | 3.11K | ± 87.97 | ops/s | 1.5x slower |
| openTelemetryClassic | 596.68 | ± 21.12 | ops/s | 7.7x slower |
| openTelemetryExponential | 500.76 | ± 15.98 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 609.30K | ± 15.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 605.58K | ± 5.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 590.09K | ± 4.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 577.61K | ± 6.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44280.310    ± 830.138  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1315.642     ± 92.155  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.769     ± 92.498  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.529      ± 9.489  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47894.707    ± 280.784  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59588.933    ± 615.643  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50962.742    ± 896.394  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5854.093    ± 236.736  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6251.301    ± 128.347  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6134.086    ± 194.650  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        596.681     ± 21.124  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        500.757     ± 15.980  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4196.542    ± 317.013  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3110.083     ± 87.968  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4601.673     ± 44.668  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     577611.488   ± 6318.107  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     590086.742   ± 4305.630  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     605575.128   ± 5243.139  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     609296.517  ± 15314.348  ops/s
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
