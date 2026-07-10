# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T07:21:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.14K | ± 727.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.03K | ± 2.65K | ops/s | 1.2x slower |
| prometheusAdd | 51.53K | ± 123.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.41K | ± 1.01K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 13.06 | ops/s | 10x slower |
| simpleclientInc | 6.58K | ± 155.15 | ops/s | 10x slower |
| simpleclientAdd | 5.92K | ± 90.82 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 208.07 | ops/s | 48x slower |
| openTelemetryInc | 1.31K | ± 145.38 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.28K | ± 17.50 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 181.31 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 32.15 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 108.60 | ops/s | 1.7x slower |
| openTelemetryClassic | 717.15 | ± 17.82 | ops/s | 7.5x slower |
| openTelemetryExponential | 578.14 | ± 16.03 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 531.40K | ± 7.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.38K | ± 10.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.54K | ± 10.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.18K | ± 5.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49405.953   ± 1006.908  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1368.633    ± 208.069  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1311.642    ± 145.385  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1280.866     ± 17.505  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51530.134    ± 123.039  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66137.977    ± 727.365  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55033.619   ± 2647.173  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5922.464     ± 90.818  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6584.866    ± 155.148  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6607.958     ± 13.058  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.146     ± 17.819  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.136     ± 16.032  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5362.302    ± 181.307  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3092.317    ± 108.597  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4454.370     ± 32.154  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508182.247   ± 5701.877  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516535.739  ± 10691.644  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525383.038  ± 10552.567  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531403.783   ± 7547.421  ops/s
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
