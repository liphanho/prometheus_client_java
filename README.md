# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-24T08:12:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.45K | ± 956.97 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 453.07 | ops/s | 1.1x slower |
| prometheusAdd | 51.50K | ± 58.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.68K | ± 2.12K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 91.67 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.46K | ± 187.01 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 238.87 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 215.58 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.33K | ± 137.04 | ops/s | 49x slower |
| openTelemetryInc | 1.23K | ± 54.79 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 274.26 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 64.55 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 165.11 | ops/s | 1.7x slower |
| openTelemetryClassic | 712.18 | ± 28.57 | ops/s | 7.3x slower |
| openTelemetryExponential | 574.00 | ± 43.03 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.54K | ± 6.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.98K | ± 8.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 504.18K | ± 6.62K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 501.66K | ± 10.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47684.652   ± 2119.419  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1437.311    ± 215.580  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1228.865     ± 54.790  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.004    ± 137.044  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51504.184     ± 58.455  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65445.863    ± 956.974  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56963.024    ± 453.069  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6198.173    ± 238.866  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6594.425     ± 91.672  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6455.298    ± 187.012  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.185     ± 28.568  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.002     ± 43.033  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5231.788    ± 274.258  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3039.927    ± 165.105  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.857     ± 64.554  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     504180.187   ± 6620.206  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     501661.427  ± 10909.529  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512983.762   ± 8304.287  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532539.817   ± 6947.309  ops/s
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
