# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-30T09:26:29Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.25K | ± 395.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 338.44 | ops/s | 1.2x slower |
| prometheusAdd | 51.16K | ± 506.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.56K | ± 995.71 | ops/s | 1.4x slower |
| simpleclientInc | 6.51K | ± 132.14 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 169.90 | ops/s | 10x slower |
| simpleclientAdd | 6.04K | ± 299.90 | ops/s | 11x slower |
| openTelemetryAdd | 1.55K | ± 251.78 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 134.75 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 31.11 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 149.54 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 39.61 | ops/s | 1.2x slower |
| prometheusNative | 2.99K | ± 186.77 | ops/s | 1.8x slower |
| openTelemetryClassic | 692.47 | ± 44.64 | ops/s | 7.7x slower |
| openTelemetryExponential | 522.04 | ± 35.05 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.16K | ± 6.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.25K | ± 10.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 465.55K | ± 5.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.98K | ± 2.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48560.449    ± 995.715  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1551.201    ± 251.783  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1250.457     ± 31.113  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1317.723    ± 134.749  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51164.567    ± 506.602  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66246.356    ± 395.159  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56971.241    ± 338.436  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6036.440    ± 299.896  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6509.264    ± 132.145  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6396.185    ± 169.896  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.466     ± 44.637  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.044     ± 35.045  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5360.530    ± 149.541  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2994.026    ± 186.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4335.362     ± 39.611  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459982.769   ± 2522.203  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465551.658   ± 5102.942  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480248.986  ± 10230.782  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486164.407   ± 6454.909  ops/s
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
