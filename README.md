# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-16T06:08:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.22K | ± 267.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.15K | ± 1.39K | ops/s | 1.2x slower |
| prometheusAdd | 51.69K | ± 315.30 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.67K | ± 1.08K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 8.20 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.43K | ± 164.62 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 209.77 | ops/s | 11x slower |
| openTelemetryInc | 1.43K | ± 178.01 | ops/s | 46x slower |
| openTelemetryAdd | 1.40K | ± 252.74 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 16.20 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 328.28 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 90.77 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 94.34 | ops/s | 1.7x slower |
| openTelemetryClassic | 653.90 | ± 33.46 | ops/s | 8.0x slower |
| openTelemetryExponential | 557.28 | ± 11.43 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.64K | ± 4.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 522.85K | ± 8.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 513.21K | ± 2.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.70K | ± 2.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49668.020   ± 1083.647  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1400.033    ± 252.743  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1429.155    ± 178.005  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1242.164     ± 16.201  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51694.125    ± 315.298  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66224.180    ± 267.864  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56148.699   ± 1391.313  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6180.088    ± 209.769  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6694.858      ± 8.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6430.769    ± 164.625  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        653.902     ± 33.459  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.285     ± 11.434  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5240.065    ± 328.284  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3153.084     ± 94.342  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.244     ± 90.772  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513208.809   ± 2971.809  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510700.273   ± 2987.046  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     522847.728   ± 8101.199  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536638.214   ± 4188.789  ops/s
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
