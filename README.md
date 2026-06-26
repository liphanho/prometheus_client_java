# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-26T07:28:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.09K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.48K | ± 2.89K | ops/s | 1.2x slower |
| prometheusAdd | 48.43K | ± 138.28 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.13K | ± 155.05 | ops/s | 1.4x slower |
| simpleclientAdd | 6.18K | ± 8.32 | ops/s | 9.7x slower |
| simpleclientInc | 6.17K | ± 162.54 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.12K | ± 286.41 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.34K | ± 84.22 | ops/s | 45x slower |
| openTelemetryInc | 1.32K | ± 99.42 | ops/s | 46x slower |
| openTelemetryAdd | 1.29K | ± 27.84 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 40.79 | ops/s | **fastest** |
| prometheusClassic | 3.74K | ± 135.92 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 99.04 | ops/s | 1.4x slower |
| openTelemetryClassic | 595.18 | ± 10.82 | ops/s | 7.3x slower |
| openTelemetryExponential | 506.36 | ± 9.93 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 613.96K | ± 4.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 606.18K | ± 3.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 588.26K | ± 2.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 573.49K | ± 5.81K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44125.831    ± 155.051  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1292.492     ± 27.837  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1317.740     ± 99.424  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1337.212     ± 84.221  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48432.931    ± 138.282  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60089.186   ± 1019.407  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49477.969   ± 2887.973  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6184.293      ± 8.322  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6169.633    ± 162.538  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6118.030    ± 286.413  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.175     ± 10.824  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        506.360      ± 9.925  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3735.555    ± 135.918  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3086.407     ± 99.040  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4369.675     ± 40.795  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     573489.572   ± 5813.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     588262.971   ± 2611.808  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     606175.256   ± 3341.545  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     613962.529   ± 4507.576  ops/s
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
