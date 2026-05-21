# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-21T07:27:34Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.90K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.99K | ± 522.64 | ops/s | 1.2x slower |
| prometheusAdd | 62.53K | ± 1.72K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.93K | ± 344.24 | ops/s | 1.4x slower |
| simpleclientInc | 8.05K | ± 139.23 | ops/s | 9.6x slower |
| simpleclientAdd | 7.58K | ± 277.12 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 7.55K | ± 112.40 | ops/s | 10x slower |
| openTelemetryAdd | 1.76K | ± 132.20 | ops/s | 44x slower |
| openTelemetryInc | 1.69K | ± 93.89 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.66K | ± 78.08 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.08K | ± 3.83 | ops/s | **fastest** |
| simpleclient | 5.59K | ± 35.84 | ops/s | 1.3x slower |
| prometheusNative | 3.99K | ± 70.39 | ops/s | 1.8x slower |
| openTelemetryClassic | 772.54 | ± 16.55 | ops/s | 9.2x slower |
| openTelemetryExponential | 690.61 | ± 21.84 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 772.07K | ± 6.88K | ops/s | **fastest** |
| prometheusWriteToByteArray | 750.05K | ± 19.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 734.58K | ± 5.98K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 716.83K | ± 6.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56929.406    ± 344.237  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1759.386    ± 132.200  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1693.849     ± 93.885  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1655.215     ± 78.077  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62528.352   ± 1715.952  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76897.627   ± 1576.894  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65985.521    ± 522.639  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7578.685    ± 277.121  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8048.375    ± 139.227  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7546.508    ± 112.404  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        772.542     ± 16.553  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        690.613     ± 21.839  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7079.807      ± 3.833  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3988.178     ± 70.387  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5593.766     ± 35.843  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     716829.651   ± 6091.570  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     734581.642   ± 5975.333  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     750051.945  ± 19041.134  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772070.970   ± 6875.869  ops/s
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
