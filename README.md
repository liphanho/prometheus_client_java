# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-06T06:46:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.31K | ± 830.00 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 1.06K | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 116.34 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.26K | ± 1.60K | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 38.11 | ops/s | 9.9x slower |
| simpleclientAdd | 6.48K | ± 16.32 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 252.50 | ops/s | 10x slower |
| openTelemetryAdd | 1.25K | ± 18.70 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.23K | ± 78.41 | ops/s | 54x slower |
| openTelemetryInc | 1.21K | ± 38.59 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.54K | ± 264.76 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 62.62 | ops/s | 1.3x slower |
| prometheusNative | 3.06K | ± 166.17 | ops/s | 1.8x slower |
| openTelemetryClassic | 685.87 | ± 32.44 | ops/s | 8.1x slower |
| openTelemetryExponential | 520.88 | ± 8.44 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.35K | ± 5.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.42K | ± 3.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.82K | ± 3.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.29K | ± 5.14K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49256.765   ± 1604.023  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1253.172     ± 18.700  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1210.391     ± 38.593  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.743     ± 78.412  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51432.135    ± 116.341  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66307.784    ± 830.004  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56246.162   ± 1058.415  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6480.002     ± 16.317  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6671.084     ± 38.109  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6452.935    ± 252.501  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.866     ± 32.436  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        520.877      ± 8.444  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5544.456    ± 264.758  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3059.451    ± 166.167  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4377.486     ± 62.620  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505285.422   ± 5136.406  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510821.062   ± 3450.822  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524420.220   ± 3683.607  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532351.431   ± 5214.816  ops/s
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
