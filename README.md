# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-31T05:53:34Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.06K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.13K | ± 632.17 | ops/s | 1.2x slower |
| prometheusAdd | 50.87K | ± 1.17K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.52K | ± 1.74K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 214.48 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 201.60 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 166.70 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.33K | ± 282.99 | ops/s | 49x slower |
| openTelemetryAdd | 1.24K | ± 46.26 | ops/s | 53x slower |
| openTelemetryInc | 1.20K | ± 35.00 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.17K | ± 75.59 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 30.73 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 204.85 | ops/s | 1.8x slower |
| openTelemetryClassic | 652.52 | ± 16.65 | ops/s | 7.9x slower |
| openTelemetryExponential | 564.03 | ± 22.62 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.76K | ± 6.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 510.34K | ± 4.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 495.82K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.08K | ± 5.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49520.240   ± 1742.889  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1235.270     ± 46.265  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1198.057     ± 35.000  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1333.037    ± 282.991  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50868.263   ± 1169.727  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65062.576   ± 1214.268  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56130.983    ± 632.175  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6185.423    ± 166.703  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6576.974    ± 214.484  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.043    ± 201.599  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.523     ± 16.649  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.031     ± 22.616  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5172.994     ± 75.590  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2943.796    ± 204.854  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4378.108     ± 30.733  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483080.770   ± 5113.140  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     495818.706   ± 3939.146  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     510336.602   ± 4477.603  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512759.528   ± 6914.492  ops/s
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
