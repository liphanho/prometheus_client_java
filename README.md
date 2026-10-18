# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-18T08:16:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.28K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.97K | ± 1.12K | ops/s | 1.2x slower |
| prometheusAdd | 50.83K | ± 623.08 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.09K | ± 1.61K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.48K | ± 191.94 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 22.29 | ops/s | 10x slower |
| simpleclientInc | 6.38K | ± 76.20 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 131.95 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.35K | ± 161.47 | ops/s | 48x slower |
| openTelemetryAdd | 1.31K | ± 33.27 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.37K | ± 440.08 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 40.96 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 171.75 | ops/s | 1.7x slower |
| openTelemetryClassic | 718.60 | ± 29.63 | ops/s | 7.5x slower |
| openTelemetryExponential | 555.73 | ± 30.93 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.72K | ± 4.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 511.10K | ± 3.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.90K | ± 6.11K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 496.46K | ± 3.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48088.698   ± 1606.087  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1309.124     ± 33.267  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.678    ± 131.954  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1347.857    ± 161.474  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50833.486    ± 623.080  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65280.992   ± 1580.100  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55970.455   ± 1118.493  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6463.977     ± 22.287  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6383.174     ± 76.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6477.249    ± 191.938  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.595     ± 29.626  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.732     ± 30.928  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5372.416    ± 440.084  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3099.301    ± 171.754  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.390     ± 40.956  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     496460.414   ± 3197.091  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506896.368   ± 6112.013  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     511102.945   ± 3391.006  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535720.277   ± 4812.257  ops/s
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
