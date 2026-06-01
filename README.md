# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-01T08:13:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.39K | ± 786.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.41K | ± 569.88 | ops/s | 1.2x slower |
| prometheusAdd | 47.91K | ± 546.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.37K | ± 536.20 | ops/s | 1.4x slower |
| simpleclientInc | 6.27K | ± 36.10 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.26K | ± 34.75 | ops/s | 9.7x slower |
| simpleclientAdd | 5.92K | ± 218.60 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 113.99 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.36K | ± 65.81 | ops/s | 44x slower |
| openTelemetryInc | 1.25K | ± 51.51 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.55K | ± 30.37 | ops/s | **fastest** |
| prometheusClassic | 4.42K | ± 832.18 | ops/s | 1.0x slower |
| prometheusNative | 3.16K | ± 103.28 | ops/s | 1.4x slower |
| openTelemetryClassic | 617.21 | ± 34.71 | ops/s | 7.4x slower |
| openTelemetryExponential | 514.11 | ± 6.91 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 644.21K | ± 4.41K | ops/s | **fastest** |
| prometheusWriteToByteArray | 625.19K | ± 4.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 605.64K | ± 7.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.24K | ± 1.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44365.349    ± 536.205  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1440.027    ± 113.986  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1254.012     ± 51.509  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.395     ± 65.807  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47909.405    ± 546.896  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60390.506    ± 786.559  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51406.172    ± 569.883  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5918.137    ± 218.605  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6265.571     ± 36.101  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6255.883     ± 34.748  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        617.214     ± 34.711  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.113      ± 6.912  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4421.917    ± 832.180  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3156.153    ± 103.278  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.822     ± 30.371  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597240.173   ± 1924.742  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     605638.912   ± 7248.953  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     625192.144   ± 4022.925  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     644214.486   ± 4405.576  ops/s
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
