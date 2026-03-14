# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-14T05:28:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.90K | ± 3.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.31K | ± 2.55K | ops/s | 1.2x slower |
| prometheusAdd | 50.52K | ± 204.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.46K | ± 1.34K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 102.80 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.58K | ± 180.05 | ops/s | 9.7x slower |
| simpleclientAdd | 6.35K | ± 178.14 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 205.26 | ops/s | 46x slower |
| openTelemetryInc | 1.29K | ± 62.38 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.27K | ± 139.28 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 292.99 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 39.65 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 169.08 | ops/s | 1.9x slower |
| openTelemetryClassic | 685.29 | ± 46.14 | ops/s | 8.2x slower |
| openTelemetryExponential | 537.11 | ± 8.92 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 548.52K | ± 1.83K | ops/s | **fastest** |
| prometheusWriteToNull | 547.41K | ± 2.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.34K | ± 3.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 517.55K | ± 2.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49463.019   ± 1340.928  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1399.804    ± 205.258  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.766     ± 62.380  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1266.689    ± 139.284  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50517.934    ± 204.054  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63896.625   ± 3402.944  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54307.377   ± 2553.620  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6347.473    ± 178.139  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6708.162    ± 102.799  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6577.302    ± 180.049  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.293     ± 46.144  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.108      ± 8.916  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5608.091    ± 292.985  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2998.206    ± 169.083  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4515.882     ± 39.648  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     517546.319   ± 2108.175  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     530340.338   ± 3072.177  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548521.711   ± 1829.617  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     547408.084   ± 2791.497  ops/s
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
