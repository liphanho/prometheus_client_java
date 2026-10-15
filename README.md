# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-15T08:19:06Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.31K | ± 665.39 | ops/s | **fastest** |
| codahaleIncNoLabels | 64.90K | ± 3.63K | ops/s | 1.1x slower |
| prometheusNoLabelsInc | 63.35K | ± 370.83 | ops/s | 1.1x slower |
| prometheusAdd | 57.33K | ± 882.76 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 10.49K | ± 435.32 | ops/s | 6.6x slower |
| simpleclientInc | 10.35K | ± 269.45 | ops/s | 6.7x slower |
| simpleclientAdd | 9.95K | ± 56.08 | ops/s | 7.0x slower |
| openTelemetryAdd | 2.17K | ± 236.38 | ops/s | 32x slower |
| openTelemetryIncNoLabels | 2.11K | ± 213.65 | ops/s | 33x slower |
| openTelemetryInc | 1.89K | ± 33.28 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.50K | ± 171.38 | ops/s | **fastest** |
| simpleclient | 7.11K | ± 149.51 | ops/s | 1.1x slower |
| prometheusNative | 5.03K | ± 365.24 | ops/s | 1.5x slower |
| openTelemetryClassic | 880.87 | ± 56.07 | ops/s | 8.5x slower |
| openTelemetryExponential | 702.64 | ± 5.12 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 788.01K | ± 39.77K | ops/s | **fastest** |
| prometheusWriteToNull | 780.10K | ± 44.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 753.44K | ± 57.41K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 721.14K | ± 19.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      64900.243   ± 3630.952  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2173.639    ± 236.378  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1887.291     ± 33.279  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2106.385    ± 213.647  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57333.755    ± 882.758  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69309.172    ± 665.394  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63346.419    ± 370.830  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9953.910     ± 56.081  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10347.114    ± 269.449  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10485.203    ± 435.318  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        880.874     ± 56.066  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        702.643      ± 5.120  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7497.189    ± 171.381  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5026.697    ± 365.240  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7105.750    ± 149.512  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     721143.637  ± 19726.485  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     753438.636  ± 57410.526  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     788013.502  ± 39774.129  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     780101.012  ± 44456.152  ops/s
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
