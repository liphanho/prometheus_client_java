# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-06T05:33:16Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.36K | ± 4.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 955.93 | ops/s | 1.1x slower |
| prometheusAdd | 51.72K | ± 117.68 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.31K | ± 1.60K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 173.44 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.57K | ± 208.61 | ops/s | 9.6x slower |
| simpleclientAdd | 6.29K | ± 215.47 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.40K | ± 153.35 | ops/s | 45x slower |
| openTelemetryAdd | 1.38K | ± 220.22 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 21.15 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.09K | ± 104.91 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 24.67 | ops/s | 1.1x slower |
| prometheusNative | 3.21K | ± 36.85 | ops/s | 1.6x slower |
| openTelemetryClassic | 693.54 | ± 29.42 | ops/s | 7.3x slower |
| openTelemetryExponential | 542.83 | ± 10.12 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 549.82K | ± 6.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.09K | ± 6.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 524.87K | ± 5.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.87K | ± 3.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49310.905   ± 1600.583  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1375.814    ± 220.224  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1263.899     ± 21.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1400.497    ± 153.353  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51719.318    ± 117.679  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63356.378   ± 4228.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56385.796    ± 955.934  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6293.042    ± 215.469  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.205    ± 173.443  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6574.296    ± 208.610  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.544     ± 29.425  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        542.834     ± 10.118  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5085.233    ± 104.913  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3212.420     ± 36.846  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.430     ± 24.665  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522870.751   ± 3728.104  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524868.384   ± 5304.339  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542090.805   ± 6220.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549819.948   ± 6901.974  ops/s
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
