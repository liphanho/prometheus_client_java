# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-10T09:26:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.41K | ± 131.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.38K | ± 2.56K | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 160.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.28K | ± 1.51K | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 142.06 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 132.41 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 230.65 | ops/s | 10x slower |
| openTelemetryAdd | 1.75K | ± 91.96 | ops/s | 38x slower |
| openTelemetryInc | 1.37K | ± 156.79 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.26K | ± 58.65 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 263.11 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 50.49 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 63.00 | ops/s | 1.7x slower |
| openTelemetryClassic | 637.99 | ± 5.93 | ops/s | 8.3x slower |
| openTelemetryExponential | 570.60 | ± 8.79 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 513.63K | ± 4.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.28K | ± 7.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.76K | ± 1.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.86K | ± 4.37K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48276.555   ± 1505.686  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1754.789     ± 91.964  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1369.182    ± 156.788  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1258.055     ± 58.653  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51469.912    ± 160.728  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66408.257    ± 131.658  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55382.693   ± 2555.704  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6327.098    ± 230.654  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6556.404    ± 142.060  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6522.305    ± 132.408  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        637.992      ± 5.933  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.600      ± 8.793  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5309.673    ± 263.107  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3093.515     ± 62.998  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.839     ± 50.485  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488864.575   ± 4370.986  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491762.917   ± 1900.409  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506278.984   ± 7255.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513634.555   ± 4900.130  ops/s
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
