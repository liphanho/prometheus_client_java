# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-13T05:39:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.49K | ± 121.55 | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 642.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.05K | ± 412.98 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.70K | ± 7.36 | ops/s | 9.7x slower |
| simpleclientInc | 6.66K | ± 197.35 | ops/s | 9.8x slower |
| simpleclientAdd | 6.35K | ± 159.24 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 266.96 | ops/s | 47x slower |
| openTelemetryAdd | 1.26K | ± 67.50 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.25K | ± 60.55 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 457.07 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 39.85 | ops/s | 1.2x slower |
| prometheusNative | 2.86K | ± 100.36 | ops/s | 1.8x slower |
| openTelemetryClassic | 711.73 | ± 21.44 | ops/s | 7.4x slower |
| openTelemetryExponential | 560.85 | ± 21.86 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.66K | ± 10.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 518.10K | ± 7.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 502.19K | ± 3.96K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 498.44K | ± 2.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50054.429    ± 412.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.687     ± 67.501  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1376.990    ± 266.964  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1248.809     ± 60.547  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51171.928    ± 642.704  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65328.385   ± 1142.951  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56490.854    ± 121.550  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6354.389    ± 159.241  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.708    ± 197.346  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6702.503      ± 7.365  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.729     ± 21.436  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.854     ± 21.856  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5264.872    ± 457.071  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2860.651    ± 100.358  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4540.609     ± 39.847  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     498442.686   ± 2629.526  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     502185.106   ± 3960.876  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     518099.816   ± 7283.964  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530662.389  ± 10538.029  ops/s
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
