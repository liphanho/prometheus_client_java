# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-06T10:14:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.20K | ± 181.39 | ops/s | **fastest** |
| prometheusInc | 30.77K | ± 1.09K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.43K | ± 1.16K | ops/s | 1.1x slower |
| prometheusAdd | 28.21K | ± 47.42 | ops/s | 1.1x slower |
| simpleclientInc | 6.58K | ± 154.77 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.28K | ± 82.14 | ops/s | 5.0x slower |
| simpleclientAdd | 5.91K | ± 198.07 | ops/s | 5.3x slower |
| openTelemetryAdd | 1.30K | ± 56.63 | ops/s | 24x slower |
| openTelemetryInc | 1.29K | ± 60.72 | ops/s | 24x slower |
| openTelemetryIncNoLabels | 1.29K | ± 123.50 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.17K | ± 62.83 | ops/s | **fastest** |
| prometheusClassic | 3.17K | ± 160.61 | ops/s | 1.3x slower |
| prometheusNative | 2.08K | ± 191.51 | ops/s | 2.0x slower |
| openTelemetryClassic | 519.84 | ± 4.04 | ops/s | 8.0x slower |
| openTelemetryExponential | 406.68 | ± 7.63 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 320.73K | ± 4.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 318.91K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 300.08K | ± 3.74K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 299.55K | ± 1.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29434.578   ± 1157.132  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1298.839     ± 56.632  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1293.187     ± 60.722  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1285.514    ± 123.503  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28208.799     ± 47.419  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30769.344   ± 1086.190  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31197.669    ± 181.386  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5911.608    ± 198.067  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6576.914    ± 154.765  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6283.076     ± 82.139  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        519.844      ± 4.041  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        406.681      ± 7.633  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3170.070    ± 160.608  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2082.006    ± 191.514  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4174.279     ± 62.831  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     299552.321   ± 1279.838  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     300076.839   ± 3740.290  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     318911.697   ± 2602.370  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     320728.094   ± 4762.393  ops/s
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
