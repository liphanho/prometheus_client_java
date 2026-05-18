# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-18T07:31:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.81K | ± 1.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.88K | ± 784.42 | ops/s | 1.2x slower |
| prometheusAdd | 47.76K | ± 91.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 38.40K | ± 9.74K | ops/s | 1.6x slower |
| simpleclientInc | 6.29K | ± 81.26 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.13K | ± 104.58 | ops/s | 9.8x slower |
| simpleclientAdd | 5.85K | ± 280.19 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 128.32 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.37K | ± 84.68 | ops/s | 44x slower |
| openTelemetryInc | 1.34K | ± 45.57 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.51K | ± 805.13 | ops/s | **fastest** |
| simpleclient | 4.14K | ± 160.69 | ops/s | 1.1x slower |
| prometheusNative | 3.12K | ± 89.18 | ops/s | 1.4x slower |
| openTelemetryClassic | 603.16 | ± 25.72 | ops/s | 7.5x slower |
| openTelemetryExponential | 511.06 | ± 18.85 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 646.03K | ± 2.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 638.21K | ± 2.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 607.99K | ± 3.29K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 604.20K | ± 2.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      38403.461   ± 9735.371  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1397.063    ± 128.320  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1336.349     ± 45.575  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1365.197     ± 84.683  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47759.551     ± 91.963  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59809.830   ± 1247.798  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51879.173    ± 784.423  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5854.388    ± 280.187  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6285.743     ± 81.265  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6131.967    ± 104.583  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        603.162     ± 25.716  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        511.059     ± 18.850  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4508.946    ± 805.132  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3121.330     ± 89.183  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4138.468    ± 160.690  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     604203.462   ± 2199.620  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     607989.846   ± 3291.756  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     638211.730   ± 2923.430  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     646031.634   ± 2793.201  ops/s
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
