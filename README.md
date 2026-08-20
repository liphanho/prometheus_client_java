# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T04:13:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.24K | ± 954.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.32K | ± 116.24 | ops/s | 1.2x slower |
| prometheusAdd | 51.03K | ± 249.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.17K | ± 1.70K | ops/s | 1.4x slower |
| simpleclientInc | 6.48K | ± 182.42 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.46K | ± 161.96 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 182.42 | ops/s | 11x slower |
| openTelemetryAdd | 1.66K | ± 287.48 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.39K | ± 264.46 | ops/s | 48x slower |
| openTelemetryInc | 1.25K | ± 61.62 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 195.13 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 61.92 | ops/s | 1.3x slower |
| prometheusNative | 3.08K | ± 138.11 | ops/s | 1.8x slower |
| openTelemetryClassic | 691.08 | ± 17.91 | ops/s | 8.1x slower |
| openTelemetryExponential | 543.12 | ± 23.26 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 520.90K | ± 5.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 514.73K | ± 11.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.96K | ± 4.02K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 477.73K | ± 3.45K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48170.049   ± 1699.712  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1663.200    ± 287.482  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1253.006     ± 61.624  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1387.427    ± 264.458  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51027.862    ± 249.508  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66241.480    ± 954.866  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56316.066    ± 116.239  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6209.626    ± 182.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6479.160    ± 182.422  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6458.994    ± 161.963  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.083     ± 17.915  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.122     ± 23.261  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5607.576    ± 195.128  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3078.651    ± 138.113  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.451     ± 61.920  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477728.274   ± 3445.838  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483959.579   ± 4019.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     514729.137  ± 11024.763  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     520901.012   ± 5715.445  ops/s
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
