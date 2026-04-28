# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-28T06:48:28Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.97K | ± 1.87K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 1.02K | ops/s | 1.2x slower |
| prometheusAdd | 51.48K | ± 254.44 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.02K | ± 957.04 | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 14.19 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.61K | ± 16.71 | ops/s | 9.8x slower |
| simpleclientAdd | 6.13K | ± 307.07 | ops/s | 11x slower |
| openTelemetryAdd | 1.58K | ± 209.83 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.41K | ± 164.73 | ops/s | 46x slower |
| openTelemetryInc | 1.31K | ± 60.44 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.93K | ± 116.20 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 99.76 | ops/s | 1.1x slower |
| prometheusNative | 2.90K | ± 104.47 | ops/s | 1.7x slower |
| openTelemetryClassic | 674.98 | ± 23.89 | ops/s | 7.3x slower |
| openTelemetryExponential | 600.24 | ± 28.83 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.83K | ± 8.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.41K | ± 6.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.32K | ± 8.53K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.59K | ± 5.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49018.123    ± 957.039  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1582.893    ± 209.829  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1307.041     ± 60.436  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1408.949    ± 164.726  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51476.460    ± 254.436  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64969.373   ± 1866.288  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56245.016   ± 1016.853  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6131.819    ± 307.066  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6704.500     ± 14.185  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6607.496     ± 16.711  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.976     ± 23.887  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        600.236     ± 28.826  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4931.660    ± 116.195  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2899.519    ± 104.471  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4362.810     ± 99.765  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508585.927   ± 5057.525  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514324.531   ± 8531.936  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526414.922   ± 6797.206  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537831.027   ± 8242.248  ops/s
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
