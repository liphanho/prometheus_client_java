# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-22T07:25:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.40K | ± 2.09K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.15K | ± 401.18 | ops/s | 1.1x slower |
| prometheusAdd | 48.60K | ± 1.07K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.99K | ± 166.64 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 61.42 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.99K | ± 246.41 | ops/s | 9.6x slower |
| simpleclientAdd | 5.76K | ± 124.14 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.58K | ± 10.93 | ops/s | 36x slower |
| openTelemetryInc | 1.46K | ± 71.74 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.40K | ± 57.16 | ops/s | 41x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.42K | ± 298.81 | ops/s | **fastest** |
| simpleclient | 4.29K | ± 81.00 | ops/s | 1.0x slower |
| prometheusNative | 3.01K | ± 30.19 | ops/s | 1.5x slower |
| openTelemetryClassic | 596.87 | ± 17.39 | ops/s | 7.4x slower |
| openTelemetryExponential | 530.75 | ± 27.09 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 625.85K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 604.83K | ± 10.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 590.32K | ± 5.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 576.32K | ± 6.00K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43988.707    ± 166.639  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1577.133     ± 10.928  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1464.816     ± 71.742  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1401.447     ± 57.156  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48602.379   ± 1073.364  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57395.226   ± 2085.103  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51146.181    ± 401.181  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5760.261    ± 124.141  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6161.953     ± 61.421  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5991.926    ± 246.411  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        596.871     ± 17.393  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.749     ± 27.089  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4415.800    ± 298.808  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3011.860     ± 30.194  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4292.628     ± 81.004  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     576321.118   ± 5995.687  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     590324.401   ± 5219.174  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     604834.845  ± 10562.832  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     625849.083   ± 3595.431  ops/s
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
