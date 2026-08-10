# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-10T05:12:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.28K | ± 3.27K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.46K | ± 626.18 | ops/s | 1.1x slower |
| prometheusAdd | 63.00K | ± 1.14K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.08K | ± 572.09 | ops/s | 1.3x slower |
| simpleclientInc | 8.10K | ± 11.63 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 8.07K | ± 28.73 | ops/s | 9.3x slower |
| simpleclientAdd | 7.68K | ± 321.77 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.87K | ± 179.93 | ops/s | 40x slower |
| openTelemetryInc | 1.65K | ± 78.72 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.59K | ± 68.76 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.78K | ± 55.94 | ops/s | **fastest** |
| simpleclient | 5.82K | ± 174.48 | ops/s | 1.2x slower |
| prometheusNative | 4.04K | ± 59.48 | ops/s | 1.7x slower |
| openTelemetryClassic | 774.74 | ± 37.45 | ops/s | 8.7x slower |
| openTelemetryExponential | 672.19 | ± 20.43 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 779.68K | ± 10.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 761.75K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 740.92K | ± 3.14K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 720.12K | ± 4.78K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57082.317    ± 572.090  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1868.284    ± 179.926  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1648.043     ± 78.719  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1590.514     ± 68.764  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62995.619   ± 1141.321  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75275.451   ± 3268.945  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66459.988    ± 626.181  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7676.031    ± 321.770  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8100.105     ± 11.633  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8072.080     ± 28.729  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        774.741     ± 37.451  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        672.191     ± 20.429  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6778.978     ± 55.944  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4039.862     ± 59.484  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5816.717    ± 174.479  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     720121.352   ± 4782.571  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     740915.515   ± 3136.896  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     761753.453   ± 5562.069  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     779682.327  ± 10272.931  ops/s
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
