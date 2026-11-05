# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-05T10:18:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.41K | ± 567.07 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.19K | ± 1.26K | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 263.34 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.87K | ± 1.14K | ops/s | 1.4x slower |
| simpleclientInc | 6.61K | ± 8.88 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.26K | ± 201.90 | ops/s | 11x slower |
| simpleclientAdd | 5.89K | ± 105.65 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 220.00 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.25K | ± 104.18 | ops/s | 53x slower |
| openTelemetryInc | 1.23K | ± 103.70 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 143.36 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 61.88 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 42.70 | ops/s | 1.7x slower |
| openTelemetryClassic | 664.85 | ± 22.99 | ops/s | 7.9x slower |
| openTelemetryExponential | 557.66 | ± 16.72 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 466.70K | ± 4.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 461.65K | ± 9.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 441.51K | ± 4.60K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 431.21K | ± 5.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48871.749   ± 1135.299  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1507.071    ± 220.001  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1230.794    ± 103.701  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1250.830    ± 104.177  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51362.471    ± 263.345  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66405.318    ± 567.069  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56190.510   ± 1261.373  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5890.198    ± 105.650  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6606.061      ± 8.878  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6259.812    ± 201.900  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        664.849     ± 22.993  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.657     ± 16.719  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5254.253    ± 143.358  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3126.257     ± 42.701  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.340     ± 61.883  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     431211.997   ± 5377.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     441512.532   ± 4596.843  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     461652.647   ± 9068.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     466699.841   ± 4785.530  ops/s
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
