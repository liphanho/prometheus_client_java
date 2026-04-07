# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-07T05:50:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.63K | ± 989.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.70K | ± 409.24 | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 288.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.46K | ± 1.44K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 18.36 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.38K | ± 181.08 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 211.70 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 235.07 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.34K | ± 138.26 | ops/s | 49x slower |
| openTelemetryInc | 1.29K | ± 18.44 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 254.92 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 31.97 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 102.75 | ops/s | 1.8x slower |
| openTelemetryClassic | 686.87 | ± 16.53 | ops/s | 7.8x slower |
| openTelemetryExponential | 564.63 | ± 15.69 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 543.24K | ± 2.41K | ops/s | **fastest** |
| prometheusWriteToByteArray | 530.15K | ± 11.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.12K | ± 5.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 512.06K | ± 3.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48455.335   ± 1440.464  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1434.375    ± 235.070  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1293.177     ± 18.438  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1339.008    ± 138.261  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51549.454    ± 288.899  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65629.074    ± 989.163  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56699.052    ± 409.245  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6197.076    ± 211.701  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.262     ± 18.360  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6384.358    ± 181.085  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.867     ± 16.527  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.625     ± 15.691  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5335.829    ± 254.917  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2974.830    ± 102.749  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.468     ± 31.975  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     512055.848   ± 3337.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520117.641   ± 5394.339  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530147.655  ± 11360.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     543244.477   ± 2408.308  ops/s
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
