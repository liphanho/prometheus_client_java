# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-02T05:42:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.57K | ± 10.08 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.47K | ± 874.70 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.90K | ± 941.52 | ops/s | 1.1x slower |
| prometheusAdd | 28.61K | ± 168.37 | ops/s | 1.1x slower |
| simpleclientInc | 6.95K | ± 106.10 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.91K | ± 250.41 | ops/s | 4.6x slower |
| simpleclientAdd | 6.64K | ± 140.63 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.44K | ± 80.20 | ops/s | 22x slower |
| openTelemetryInc | 1.41K | ± 98.62 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.35K | ± 69.84 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.60K | ± 51.20 | ops/s | **fastest** |
| prometheusClassic | 3.11K | ± 151.59 | ops/s | 1.5x slower |
| prometheusNative | 2.32K | ± 212.17 | ops/s | 2.0x slower |
| openTelemetryClassic | 520.04 | ± 31.77 | ops/s | 8.8x slower |
| openTelemetryExponential | 401.90 | ± 10.01 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 339.61K | ± 3.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 337.31K | ± 2.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.04K | ± 1.96K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 310.56K | ± 1.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29896.246    ± 941.523  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1444.401     ± 80.197  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1405.442     ± 98.623  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1352.878     ± 69.839  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28608.410    ± 168.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31565.852     ± 10.076  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30469.330    ± 874.699  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6639.540    ± 140.630  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6945.387    ± 106.101  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6914.498    ± 250.412  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        520.039     ± 31.766  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        401.897     ± 10.011  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3107.727    ± 151.587  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2318.255    ± 212.172  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4599.535     ± 51.205  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     310563.905   ± 1609.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     312035.971   ± 1963.221  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     337305.469   ± 2428.344  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     339611.862   ± 3210.672  ops/s
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
