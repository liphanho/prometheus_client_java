# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-23T05:42:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.53K | ± 800.85 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 411.26 | ops/s | 1.2x slower |
| prometheusAdd | 51.66K | ± 80.92 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.33K | ± 141.32 | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 37.47 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.45K | ± 209.78 | ops/s | 10x slower |
| simpleclientAdd | 6.40K | ± 254.03 | ops/s | 10x slower |
| openTelemetryAdd | 1.71K | ± 101.44 | ops/s | 39x slower |
| openTelemetryInc | 1.23K | ± 31.39 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.22K | ± 42.96 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 5.20 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 135.26 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 117.44 | ops/s | 1.7x slower |
| openTelemetryClassic | 656.53 | ± 23.35 | ops/s | 8.0x slower |
| openTelemetryExponential | 551.48 | ± 37.57 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.95K | ± 7.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.56K | ± 2.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.75K | ± 8.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.65K | ± 7.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50333.987    ± 141.321  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1708.609    ± 101.437  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1228.953     ± 31.386  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1222.007     ± 42.957  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51661.786     ± 80.920  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66528.474    ± 800.845  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56876.733    ± 411.263  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6397.702    ± 254.031  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6769.963     ± 37.469  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6449.635    ± 209.776  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        656.529     ± 23.353  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.479     ± 37.572  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5260.525      ± 5.200  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.795    ± 117.442  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.191    ± 135.255  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506649.315   ± 7495.172  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512747.302   ± 8712.814  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526562.355   ± 2683.247  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537950.741   ± 7723.462  ops/s
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
