# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-24T08:34:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.41K | ± 3.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.85K | ± 511.28 | ops/s | 1.1x slower |
| prometheusAdd | 51.27K | ± 380.79 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.18K | ± 890.74 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 82.83 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.46K | ± 221.50 | ops/s | 9.8x slower |
| simpleclientAdd | 6.17K | ± 216.58 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 239.61 | ops/s | 46x slower |
| openTelemetryInc | 1.36K | ± 140.50 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.23K | ± 32.51 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 29.39 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 70.21 | ops/s | 1.2x slower |
| prometheusNative | 3.19K | ± 93.11 | ops/s | 1.6x slower |
| openTelemetryClassic | 681.55 | ± 10.46 | ops/s | 7.7x slower |
| openTelemetryExponential | 540.47 | ± 17.05 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.03K | ± 4.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.43K | ± 1.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.67K | ± 6.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.21K | ± 6.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50182.248    ± 890.742  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1369.277    ± 239.613  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1360.246    ± 140.504  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.812     ± 32.506  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51269.581    ± 380.794  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63405.561   ± 3807.230  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55852.738    ± 511.277  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6170.052    ± 216.585  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6583.749     ± 82.829  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6458.325    ± 221.501  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.547     ± 10.464  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.473     ± 17.047  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5258.121     ± 29.393  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3187.144     ± 93.109  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.588     ± 70.208  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506210.972   ± 6209.687  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508671.441   ± 6598.996  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524434.844   ± 1865.105  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533032.389   ± 4864.198  ops/s
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
