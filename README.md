# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-24T06:37:36Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.54K | ± 1.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.28K | ± 1.40K | ops/s | 1.1x slower |
| prometheusAdd | 51.06K | ± 620.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.40K | ± 1.72K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 65.25 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.36K | ± 127.51 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 232.31 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.42K | ± 103.79 | ops/s | 45x slower |
| openTelemetryAdd | 1.37K | ± 289.65 | ops/s | 47x slower |
| openTelemetryInc | 1.32K | ± 89.55 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 187.89 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 65.60 | ops/s | 1.3x slower |
| prometheusNative | 2.88K | ± 187.11 | ops/s | 1.9x slower |
| openTelemetryClassic | 667.76 | ± 43.14 | ops/s | 8.3x slower |
| openTelemetryExponential | 557.37 | ± 23.71 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.35K | ± 2.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.83K | ± 2.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.51K | ± 8.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 503.81K | ± 6.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49397.744   ± 1723.190  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1367.059    ± 289.648  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1320.408     ± 89.554  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1422.739    ± 103.785  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51062.161    ± 620.143  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64537.553   ± 1175.159  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56281.239   ± 1404.949  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6163.308    ± 232.309  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6648.385     ± 65.246  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6358.357    ± 127.506  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        667.765     ± 43.137  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.369     ± 23.714  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5529.340    ± 187.894  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2878.692    ± 187.105  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4360.404     ± 65.597  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     503814.071   ± 6089.594  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519511.533   ± 8155.805  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529829.631   ± 2569.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539349.211   ± 2828.916  ops/s
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
