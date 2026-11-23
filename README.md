# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-23T11:39:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.07K | ± 1.78K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 361.66 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 132.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.61K | ± 1.97K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 166.59 | ops/s | 10x slower |
| simpleclientAdd | 6.39K | ± 15.39 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 194.37 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 213.30 | ops/s | 45x slower |
| openTelemetryInc | 1.33K | ± 54.60 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.30K | ± 135.19 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.58K | ± 337.94 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 30.57 | ops/s | 1.3x slower |
| prometheusNative | 3.02K | ± 193.54 | ops/s | 1.8x slower |
| openTelemetryClassic | 702.65 | ± 23.69 | ops/s | 7.9x slower |
| openTelemetryExponential | 557.05 | ± 49.63 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.98K | ± 10.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.14K | ± 2.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.21K | ± 2.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.47K | ± 5.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49607.436   ± 1970.625  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.783    ± 213.302  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1326.709     ± 54.599  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1300.104    ± 135.195  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51428.375    ± 132.269  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65065.349   ± 1775.212  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56881.953    ± 361.655  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6388.288     ± 15.391  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6464.162    ± 166.588  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6364.079    ± 194.372  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.653     ± 23.690  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.051     ± 49.631  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5581.509    ± 337.939  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.579    ± 193.535  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4368.516     ± 30.571  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467472.100   ± 5464.646  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483206.238   ± 2441.021  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494141.887   ± 2873.965  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499977.758  ± 10046.984  ops/s
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
