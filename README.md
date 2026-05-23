# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-23T06:56:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.03K | ± 79.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.59K | ± 560.71 | ops/s | 1.1x slower |
| prometheusAdd | 49.41K | ± 724.78 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.54K | ± 702.33 | ops/s | 1.3x slower |
| simpleclientInc | 6.21K | ± 111.00 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.02K | ± 202.97 | ops/s | 9.8x slower |
| simpleclientAdd | 5.68K | ± 193.13 | ops/s | 10x slower |
| openTelemetryInc | 1.39K | ± 57.91 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.36K | ± 45.35 | ops/s | 44x slower |
| openTelemetryAdd | 1.31K | ± 113.90 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 3.02 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 49.12 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 64.71 | ops/s | 1.7x slower |
| openTelemetryClassic | 625.94 | ± 30.17 | ops/s | 8.3x slower |
| openTelemetryExponential | 509.15 | ± 10.19 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 626.40K | ± 4.62K | ops/s | **fastest** |
| prometheusWriteToByteArray | 608.86K | ± 7.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 592.76K | ± 2.28K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 578.08K | ± 3.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44537.043    ± 702.332  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1305.618    ± 113.905  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1392.510     ± 57.914  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1356.766     ± 45.350  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49407.442    ± 724.779  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59026.637     ± 79.547  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51588.802    ± 560.707  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5682.014    ± 193.134  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6207.826    ± 110.999  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6023.615    ± 202.975  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        625.938     ± 30.171  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        509.148     ± 10.188  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5224.907      ± 3.021  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3051.704     ± 64.708  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4339.356     ± 49.120  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     578079.306   ± 3060.163  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     592763.827   ± 2284.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     608857.265   ± 7702.925  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     626404.695   ± 4623.181  ops/s
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
