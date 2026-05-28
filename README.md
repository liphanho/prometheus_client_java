# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-28T07:29:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.70K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.38K | ± 409.74 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.31K | ± 1.42K | ops/s | 1.4x slower |
| prometheusAdd | 41.51K | ± 10.78K | ops/s | 1.4x slower |
| simpleclientInc | 6.08K | ± 115.60 | ops/s | 9.8x slower |
| simpleclientAdd | 5.93K | ± 183.65 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.87K | ± 304.04 | ops/s | 10x slower |
| openTelemetryInc | 1.32K | ± 117.18 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.29K | ± 13.53 | ops/s | 46x slower |
| openTelemetryAdd | 1.29K | ± 35.31 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.51K | ± 35.65 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 54.67 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 155.11 | ops/s | 1.8x slower |
| openTelemetryClassic | 615.13 | ± 22.30 | ops/s | 9.0x slower |
| openTelemetryExponential | 545.32 | ± 22.07 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 610.90K | ± 2.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 601.93K | ± 2.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 571.72K | ± 6.76K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 567.94K | ± 12.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43310.497   ± 1420.243  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1289.237     ± 35.305  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1316.503    ± 117.178  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1292.654     ± 13.526  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      41506.607  ± 10781.221  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59700.078   ± 1577.423  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51376.534    ± 409.741  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5929.824    ± 183.647  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6075.196    ± 115.601  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5868.736    ± 304.044  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        615.126     ± 22.296  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.325     ± 22.070  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5508.384     ± 35.652  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3100.780    ± 155.105  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4540.034     ± 54.669  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     571717.874   ± 6762.784  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     567939.094  ± 12603.294  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     601928.493   ± 2991.890  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     610895.214   ± 2448.540  ops/s
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
