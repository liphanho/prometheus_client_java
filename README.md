# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T04:21:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.22K | ± 1.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.79K | ± 836.15 | ops/s | 1.1x slower |
| prometheusAdd | 49.11K | ± 1.09K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.87K | ± 182.66 | ops/s | 1.3x slower |
| simpleclientInc | 6.28K | ± 144.33 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.05K | ± 230.70 | ops/s | 9.6x slower |
| simpleclientAdd | 5.75K | ± 197.55 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 70.36 | ops/s | 40x slower |
| openTelemetryInc | 1.37K | ± 157.69 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.32K | ± 50.63 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.96K | ± 418.70 | ops/s | **fastest** |
| simpleclient | 4.58K | ± 61.40 | ops/s | 1.1x slower |
| prometheusNative | 3.13K | ± 75.42 | ops/s | 1.6x slower |
| openTelemetryClassic | 651.22 | ± 17.82 | ops/s | 7.6x slower |
| openTelemetryExponential | 537.27 | ± 25.54 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 640.93K | ± 3.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 623.03K | ± 3.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 599.47K | ± 5.08K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 589.71K | ± 4.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43874.592    ± 182.661  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1466.276     ± 70.359  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1370.333    ± 157.693  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1318.279     ± 50.629  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49107.607   ± 1091.221  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58223.412   ± 1771.346  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51785.189    ± 836.152  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5751.977    ± 197.551  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6280.933    ± 144.329  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6049.673    ± 230.698  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.220     ± 17.818  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.268     ± 25.537  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4956.304    ± 418.704  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3133.685     ± 75.424  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4579.156     ± 61.395  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     589706.699   ± 4730.307  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     599465.994   ± 5083.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     623031.524   ± 3873.663  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     640932.748   ± 3758.366  ops/s
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
