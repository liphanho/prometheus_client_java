# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-20T06:30:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.10K | ± 4.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 429.36 | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 218.36 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.05K | ± 916.34 | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 96.06 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.50K | ± 190.11 | ops/s | 9.7x slower |
| simpleclientAdd | 6.01K | ± 47.17 | ops/s | 11x slower |
| openTelemetryAdd | 1.33K | ± 208.34 | ops/s | 47x slower |
| openTelemetryInc | 1.30K | ± 105.27 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.19K | ± 26.61 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 308.37 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 36.05 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 120.42 | ops/s | 1.8x slower |
| openTelemetryClassic | 658.04 | ± 14.13 | ops/s | 8.2x slower |
| openTelemetryExponential | 576.37 | ± 40.34 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 522.90K | ± 6.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.53K | ± 4.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 513.53K | ± 6.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.97K | ± 3.63K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49047.781    ± 916.337  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1328.573    ± 208.341  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.016    ± 105.270  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1193.718     ± 26.612  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51490.131    ± 218.355  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63104.814   ± 4758.247  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56847.149    ± 429.357  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6009.314     ± 47.174  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6598.211     ± 96.063  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6497.225    ± 190.112  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        658.036     ± 14.129  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        576.370     ± 40.336  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5406.967    ± 308.369  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3009.461    ± 120.418  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.612     ± 36.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499967.221   ± 3629.397  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     513533.609   ± 6477.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517533.144   ± 4553.187  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     522899.581   ± 6206.709  ops/s
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
