# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-12T07:59:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.01K | ± 77.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.08K | ± 505.81 | ops/s | 1.1x slower |
| prometheusAdd | 48.00K | ± 919.36 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.25K | ± 1.20K | ops/s | 1.4x slower |
| simpleclientInc | 6.35K | ± 22.85 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.25K | ± 29.73 | ops/s | 9.4x slower |
| simpleclientAdd | 6.04K | ± 179.51 | ops/s | 9.8x slower |
| openTelemetryInc | 1.38K | ± 96.65 | ops/s | 43x slower |
| openTelemetryAdd | 1.36K | ± 86.61 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 21.23 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.69K | ± 825.26 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 37.79 | ops/s | 1.0x slower |
| prometheusNative | 3.08K | ± 110.03 | ops/s | 1.5x slower |
| openTelemetryClassic | 606.60 | ± 19.23 | ops/s | 7.7x slower |
| openTelemetryExponential | 508.87 | ± 30.84 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 642.22K | ± 4.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 627.59K | ± 7.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 606.99K | ± 8.11K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.98K | ± 4.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43251.019   ± 1199.286  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1356.597     ± 86.612  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1378.155     ± 96.646  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.521     ± 21.228  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47998.392    ± 919.358  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59011.003     ± 77.213  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52081.539    ± 505.811  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6041.793    ± 179.506  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6347.762     ± 22.847  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6253.314     ± 29.726  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        606.603     ± 19.226  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        508.870     ± 30.838  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4686.343    ± 825.263  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3077.452    ± 110.033  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4550.588     ± 37.791  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597977.656   ± 4114.999  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     606986.518   ± 8110.324  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     627589.446   ± 7875.080  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     642221.904   ± 4146.361  ops/s
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
