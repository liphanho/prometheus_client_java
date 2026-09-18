# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-18T08:24:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 998.10 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 376.74 | ops/s | 1.2x slower |
| prometheusAdd | 51.30K | ± 156.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.38K | ± 7.80K | ops/s | 1.5x slower |
| simpleclientInc | 6.57K | ± 195.20 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 186.94 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 230.64 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 208.00 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 147.91 | ops/s | 51x slower |
| openTelemetryInc | 1.22K | ± 58.15 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 94.38 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 65.70 | ops/s | 1.2x slower |
| prometheusNative | 2.88K | ± 81.16 | ops/s | 1.8x slower |
| openTelemetryClassic | 686.96 | ± 49.49 | ops/s | 7.7x slower |
| openTelemetryExponential | 568.51 | ± 48.71 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.11K | ± 7.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 520.85K | ± 2.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.15K | ± 2.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 501.75K | ± 6.18K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43378.240   ± 7795.827  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1372.884    ± 208.005  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1221.991     ± 58.155  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.161    ± 147.910  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51296.219    ± 156.062  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66404.154    ± 998.100  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56783.211    ± 376.739  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6318.581    ± 230.638  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6570.781    ± 195.197  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6396.401    ± 186.944  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.960     ± 49.486  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.513     ± 48.711  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5291.338     ± 94.383  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2883.285     ± 81.162  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.833     ± 65.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501753.695   ± 6183.460  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505149.032   ± 2277.530  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     520845.647   ± 2800.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530106.502   ± 7973.365  ops/s
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
