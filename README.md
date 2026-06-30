# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-30T07:29:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.45K | ± 1.47K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.81K | ± 374.40 | ops/s | 1.1x slower |
| prometheusAdd | 51.19K | ± 312.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.28K | ± 895.72 | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 11.80 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.58K | ± 29.45 | ops/s | 9.8x slower |
| simpleclientAdd | 6.33K | ± 179.73 | ops/s | 10x slower |
| openTelemetryInc | 1.43K | ± 64.66 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.33K | ± 146.28 | ops/s | 49x slower |
| openTelemetryAdd | 1.28K | ± 76.28 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.01K | ± 11.38 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 37.27 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 137.37 | ops/s | 1.7x slower |
| openTelemetryClassic | 662.38 | ± 29.72 | ops/s | 7.6x slower |
| openTelemetryExponential | 564.37 | ± 48.12 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 525.16K | ± 4.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 516.05K | ± 4.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.30K | ± 2.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 497.85K | ± 4.36K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49275.742    ± 895.717  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1280.307     ± 76.284  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.317     ± 64.662  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.620    ± 146.280  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51189.625    ± 312.251  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64448.054   ± 1474.731  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56810.773    ± 374.402  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6326.963    ± 179.734  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6708.630     ± 11.797  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6581.306     ± 29.446  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.379     ± 29.721  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.366     ± 48.119  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5005.404     ± 11.378  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.668    ± 137.370  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.024     ± 37.270  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497847.792   ± 4363.954  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505297.241   ± 2222.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     516047.989   ± 4136.949  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     525163.378   ± 4778.781  ops/s
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
