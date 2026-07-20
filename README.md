# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-20T06:56:56Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 52.01K | ± 6.19K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.97K | ± 37.92 | ops/s | 1.0x slower |
| prometheusAdd | 48.17K | ± 357.43 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 44.19K | ± 201.45 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 6.23K | ± 68.51 | ops/s | 8.4x slower |
| simpleclientInc | 6.12K | ± 116.60 | ops/s | 8.5x slower |
| simpleclientAdd | 5.93K | ± 314.39 | ops/s | 8.8x slower |
| openTelemetryInc | 1.51K | ± 163.07 | ops/s | 34x slower |
| openTelemetryAdd | 1.42K | ± 93.68 | ops/s | 37x slower |
| openTelemetryIncNoLabels | 1.39K | ± 110.12 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 93.10 | ops/s | **fastest** |
| prometheusClassic | 4.43K | ± 809.58 | ops/s | 1.0x slower |
| prometheusNative | 3.03K | ± 89.58 | ops/s | 1.5x slower |
| openTelemetryClassic | 601.21 | ± 23.02 | ops/s | 7.4x slower |
| openTelemetryExponential | 540.36 | ± 14.39 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 642.09K | ± 4.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.83K | ± 10.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 606.59K | ± 2.36K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.16K | ± 4.64K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44191.758    ± 201.449  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1418.987     ± 93.682  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1512.718    ± 163.065  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1387.651    ± 110.121  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48169.174    ± 357.431  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      52007.992   ± 6191.858  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50973.395     ± 37.921  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5931.824    ± 314.393  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6116.332    ± 116.605  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6225.601     ± 68.514  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        601.212     ± 23.022  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.356     ± 14.388  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4428.728    ± 809.585  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3028.909     ± 89.576  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.352     ± 93.101  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597158.818   ± 4637.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     606592.978   ± 2357.782  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630826.324  ± 10548.284  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     642088.880   ± 4299.899  ops/s
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
