# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-16T08:03:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.66K | ± 405.11 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 328.40 | ops/s | 1.2x slower |
| prometheusAdd | 51.51K | ± 143.75 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.88K | ± 1.09K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 17.07 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.46K | ± 263.38 | ops/s | 10x slower |
| simpleclientAdd | 6.45K | ± 13.20 | ops/s | 10x slower |
| openTelemetryInc | 1.33K | ± 120.27 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.32K | ± 156.63 | ops/s | 50x slower |
| openTelemetryAdd | 1.23K | ± 2.65 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 22.99 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 60.02 | ops/s | 1.2x slower |
| prometheusNative | 2.93K | ± 167.60 | ops/s | 1.8x slower |
| openTelemetryClassic | 708.68 | ± 31.41 | ops/s | 7.4x slower |
| openTelemetryExponential | 585.20 | ± 40.99 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.26K | ± 6.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.12K | ± 10.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.90K | ± 3.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.01K | ± 3.43K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48883.732   ± 1093.797  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1229.308      ± 2.654  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1325.993    ± 120.273  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1323.970    ± 156.627  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51506.380    ± 143.753  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66657.133    ± 405.111  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56892.003    ± 328.402  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6451.816     ± 13.202  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6686.225     ± 17.068  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6463.373    ± 263.382  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.681     ± 31.410  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.200     ± 40.988  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5233.538     ± 22.991  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2933.572    ± 167.604  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4425.868     ± 60.016  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508895.824   ± 3842.226  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506010.658   ± 3427.414  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523117.122  ± 10963.669  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529263.729   ± 6228.088  ops/s
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
