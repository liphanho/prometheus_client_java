# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T06:36:49Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 62.96K | ± 3.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.16K | ± 176.29 | ops/s | 1.1x slower |
| prometheusAdd | 51.11K | ± 552.78 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.73K | ± 590.52 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.62K | ± 13.77 | ops/s | 9.5x slower |
| simpleclientInc | 6.59K | ± 197.41 | ops/s | 9.6x slower |
| simpleclientAdd | 6.15K | ± 257.11 | ops/s | 10x slower |
| openTelemetryAdd | 1.55K | ± 181.51 | ops/s | 41x slower |
| openTelemetryInc | 1.34K | ± 166.78 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 55.88 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 242.22 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 35.96 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 182.04 | ops/s | 1.8x slower |
| openTelemetryClassic | 676.87 | ± 23.63 | ops/s | 7.8x slower |
| openTelemetryExponential | 562.02 | ± 33.09 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.57K | ± 1.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 535.07K | ± 4.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.21K | ± 4.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.69K | ± 6.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47733.094    ± 590.521  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1545.978    ± 181.507  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.739    ± 166.785  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1235.809     ± 55.876  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51107.580    ± 552.776  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      62960.704   ± 3552.922  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57160.863    ± 176.286  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6151.852    ± 257.107  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.859    ± 197.410  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6622.356     ± 13.766  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.870     ± 23.627  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.023     ± 33.088  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5306.092    ± 242.221  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2965.630    ± 182.038  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4387.032     ± 35.959  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515688.993   ± 6345.827  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520209.066   ± 4753.626  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     535068.197   ± 4349.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537566.202   ± 1604.088  ops/s
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
