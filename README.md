# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-04T06:52:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.30K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 216.40 | ops/s | 1.1x slower |
| prometheusAdd | 51.05K | ± 477.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.56K | ± 1.17K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 14.59 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.59K | ± 15.93 | ops/s | 9.9x slower |
| simpleclientAdd | 5.97K | ± 120.51 | ops/s | 11x slower |
| openTelemetryAdd | 1.54K | ± 239.94 | ops/s | 42x slower |
| openTelemetryInc | 1.45K | ± 165.15 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.44K | ± 177.06 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 17.01 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 18.94 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 140.18 | ops/s | 1.8x slower |
| openTelemetryClassic | 670.76 | ± 11.58 | ops/s | 7.8x slower |
| openTelemetryExponential | 583.13 | ± 33.81 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 523.91K | ± 5.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.21K | ± 4.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 493.40K | ± 7.11K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 491.54K | ± 13.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49559.155   ± 1169.159  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1544.912    ± 239.937  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1453.490    ± 165.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1439.553    ± 177.062  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51046.439    ± 477.710  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65295.465   ± 1408.467  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57051.187    ± 216.402  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5965.263    ± 120.506  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6695.973     ± 14.594  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6594.718     ± 15.931  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        670.756     ± 11.578  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.126     ± 33.811  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5201.770     ± 17.006  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2967.277    ± 140.181  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4485.353     ± 18.936  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     491542.200  ± 13474.500  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     493396.014   ± 7106.566  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513210.432   ± 4392.579  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     523910.169   ± 5595.071  ops/s
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
