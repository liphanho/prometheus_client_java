# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-03T08:10:17Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.18K | ± 3.92K | ops/s | **fastest** |
| prometheusAdd | 51.39K | ± 131.67 | ops/s | 1.2x slower |
| prometheusNoLabelsInc | 49.68K | ± 10.99K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.67K | ± 2.21K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.42K | ± 119.51 | ops/s | 9.8x slower |
| simpleclientInc | 6.32K | ± 302.88 | ops/s | 10.0x slower |
| simpleclientAdd | 6.18K | ± 219.50 | ops/s | 10x slower |
| openTelemetryAdd | 1.24K | ± 5.10 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.23K | ± 51.65 | ops/s | 51x slower |
| openTelemetryInc | 1.22K | ± 35.22 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 27.70 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 72.81 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 155.58 | ops/s | 1.7x slower |
| openTelemetryClassic | 690.13 | ± 55.67 | ops/s | 7.6x slower |
| openTelemetryExponential | 563.77 | ± 39.24 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.88K | ± 6.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.89K | ± 4.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.62K | ± 2.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.39K | ± 4.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48671.812   ± 2214.074  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1238.744      ± 5.098  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1221.888     ± 35.222  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1233.775     ± 51.653  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51394.152    ± 131.673  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63180.964   ± 3923.363  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49680.199  ± 10991.667  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6176.878    ± 219.503  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6320.392    ± 302.883  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6418.366    ± 119.507  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.134     ± 55.666  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.765     ± 39.237  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5243.240     ± 27.696  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3063.937    ± 155.582  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4477.217     ± 72.814  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505389.271   ± 4860.812  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515615.511   ± 2705.888  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533889.627   ± 4571.758  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537882.527   ± 6404.783  ops/s
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
