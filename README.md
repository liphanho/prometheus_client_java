# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-22T05:35:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.58K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 365.43 | ops/s | 1.1x slower |
| prometheusAdd | 51.38K | ± 390.23 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.43K | ± 1.57K | ops/s | 1.3x slower |
| simpleclientInc | 6.68K | ± 176.17 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.61K | ± 92.69 | ops/s | 9.8x slower |
| simpleclientAdd | 6.43K | ± 163.12 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 304.99 | ops/s | 47x slower |
| openTelemetryInc | 1.34K | ± 168.69 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.23K | ± 62.94 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 331.48 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 61.04 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 64.07 | ops/s | 1.8x slower |
| openTelemetryClassic | 689.23 | ± 18.64 | ops/s | 7.8x slower |
| openTelemetryExponential | 597.31 | ± 18.41 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.39K | ± 3.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 532.57K | ± 4.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 525.57K | ± 1.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.72K | ± 2.31K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49428.056   ± 1573.357  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1365.666    ± 304.994  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1344.864    ± 168.688  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1233.768     ± 62.942  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51379.196    ± 390.226  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64578.160   ± 1048.183  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56889.827    ± 365.434  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6430.251    ± 163.124  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6680.598    ± 176.172  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6612.191     ± 92.689  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.230     ± 18.640  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        597.309     ± 18.409  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5389.448    ± 331.478  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3009.456     ± 64.066  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.137     ± 61.041  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515723.421   ± 2310.390  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     525574.567   ± 1990.335  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     532574.072   ± 4798.094  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535388.688   ± 3857.741  ops/s
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
