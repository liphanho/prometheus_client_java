# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-28T06:31:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.93K | ± 2.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.23K | ± 402.86 | ops/s | 1.2x slower |
| prometheusAdd | 48.14K | ± 361.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.31K | ± 5.49K | ops/s | 1.5x slower |
| simpleclientInc | 6.13K | ± 112.25 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.10K | ± 241.74 | ops/s | 9.7x slower |
| simpleclientAdd | 5.74K | ± 339.12 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.29K | ± 8.41 | ops/s | 46x slower |
| openTelemetryAdd | 1.27K | ± 17.65 | ops/s | 47x slower |
| openTelemetryInc | 1.16K | ± 27.67 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 10.20 | ops/s | **fastest** |
| simpleclient | 4.60K | ± 49.43 | ops/s | 1.1x slower |
| prometheusNative | 3.10K | ± 74.71 | ops/s | 1.7x slower |
| openTelemetryClassic | 579.38 | ± 15.15 | ops/s | 9.1x slower |
| openTelemetryExponential | 500.52 | ± 1.47 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 620.25K | ± 4.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.65K | ± 3.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 584.41K | ± 3.39K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 574.94K | ± 4.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40312.967   ± 5491.448  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1265.718     ± 17.653  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1164.166     ± 27.674  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1288.627      ± 8.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48139.096    ± 361.334  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58931.337   ± 2232.982  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51234.650    ± 402.857  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5740.304    ± 339.121  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6125.935    ± 112.254  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6095.218    ± 241.742  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        579.378     ± 15.155  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        500.517      ± 1.467  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5244.007     ± 10.204  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3102.211     ± 74.711  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4596.173     ± 49.427  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     574936.561   ± 4315.718  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     584412.467   ± 3386.033  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609652.082   ± 3277.641  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     620245.252   ± 4327.815  ops/s
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
