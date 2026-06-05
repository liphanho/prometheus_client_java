# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-05T07:40:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.75K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.46K | ± 1.17K | ops/s | 1.1x slower |
| prometheusAdd | 48.78K | ± 1.55K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.09K | ± 74.96 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.11K | ± 283.19 | ops/s | 9.6x slower |
| simpleclientInc | 6.00K | ± 62.12 | ops/s | 9.8x slower |
| simpleclientAdd | 5.95K | ± 140.02 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.42K | ± 95.94 | ops/s | 41x slower |
| openTelemetryInc | 1.37K | ± 89.80 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.27K | ± 39.05 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.88K | ± 429.93 | ops/s | **fastest** |
| simpleclient | 4.24K | ± 37.04 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 150.34 | ops/s | 1.6x slower |
| openTelemetryClassic | 615.43 | ± 20.10 | ops/s | 7.9x slower |
| openTelemetryExponential | 517.55 | ± 6.34 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.72K | ± 3.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 621.76K | ± 3.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 606.98K | ± 3.80K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 592.49K | ± 4.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44089.306     ± 74.963  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1417.111     ± 95.938  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.146     ± 89.796  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1266.233     ± 39.047  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48779.873   ± 1545.285  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58749.320   ± 1146.208  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51461.641   ± 1172.634  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5946.586    ± 140.025  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5999.152     ± 62.118  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6113.781    ± 283.194  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        615.434     ± 20.105  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.555      ± 6.342  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4882.236    ± 429.927  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3095.642    ± 150.342  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4238.743     ± 37.041  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     592488.608   ± 4051.342  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     606981.435   ± 3804.284  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     621759.205   ± 3032.948  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643722.462   ± 3170.045  ops/s
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
