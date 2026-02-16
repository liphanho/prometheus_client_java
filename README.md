# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-16T05:43:26Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.44K | ± 245.46 | ops/s | **fastest** |
| prometheusInc | 30.70K | ± 1.22K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.79K | ± 816.50 | ops/s | 1.1x slower |
| prometheusAdd | 28.58K | ± 184.06 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.12K | ± 41.97 | ops/s | 4.4x slower |
| simpleclientInc | 7.10K | ± 153.46 | ops/s | 4.4x slower |
| simpleclientAdd | 6.72K | ± 215.26 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.48K | ± 60.69 | ops/s | 21x slower |
| openTelemetryAdd | 1.40K | ± 44.62 | ops/s | 22x slower |
| openTelemetryInc | 1.34K | ± 20.00 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.52K | ± 27.35 | ops/s | **fastest** |
| prometheusClassic | 3.18K | ± 218.71 | ops/s | 1.4x slower |
| prometheusNative | 2.45K | ± 20.52 | ops/s | 1.8x slower |
| openTelemetryClassic | 521.54 | ± 18.06 | ops/s | 8.7x slower |
| openTelemetryExponential | 422.26 | ± 34.01 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 335.92K | ± 2.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 332.72K | ± 3.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 308.01K | ± 2.26K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 302.56K | ± 4.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29787.319    ± 816.504  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1398.903     ± 44.620  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1337.152     ± 19.999  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1476.582     ± 60.686  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28580.198    ± 184.064  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30703.035   ± 1220.691  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31436.423    ± 245.463  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6723.706    ± 215.263  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7100.322    ± 153.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7123.631     ± 41.972  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.543     ± 18.058  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        422.260     ± 34.006  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3183.667    ± 218.714  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2451.431     ± 20.517  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.743     ± 27.347  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     302558.750   ± 4205.881  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     308013.115   ± 2264.675  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     332718.714   ± 3223.116  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     335920.709   ± 2503.249  ops/s
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
