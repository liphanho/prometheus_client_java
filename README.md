# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-19T04:13:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.98K | ± 36.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.79K | ± 909.76 | ops/s | 1.1x slower |
| prometheusAdd | 47.99K | ± 805.25 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.48K | ± 1.21K | ops/s | 1.4x slower |
| simpleclientInc | 6.30K | ± 29.96 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 5.97K | ± 208.57 | ops/s | 9.9x slower |
| simpleclientAdd | 5.82K | ± 109.63 | ops/s | 10x slower |
| openTelemetryInc | 1.33K | ± 53.13 | ops/s | 44x slower |
| openTelemetryAdd | 1.31K | ± 95.28 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.31K | ± 87.01 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.61K | ± 94.81 | ops/s | **fastest** |
| prometheusClassic | 3.99K | ± 327.79 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 117.76 | ops/s | 1.5x slower |
| openTelemetryClassic | 572.16 | ± 6.55 | ops/s | 8.1x slower |
| openTelemetryExponential | 503.72 | ± 21.19 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 644.39K | ± 2.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 634.32K | ± 3.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 610.17K | ± 3.88K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.79K | ± 7.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43476.047   ± 1211.097  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1308.363     ± 95.280  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1328.431     ± 53.131  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1307.114     ± 87.010  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47992.388    ± 805.247  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58980.082     ± 36.185  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51792.874    ± 909.764  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5817.310    ± 109.626  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6298.270     ± 29.960  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5973.818    ± 208.568  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        572.160      ± 6.553  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        503.718     ± 21.186  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3988.151    ± 327.793  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3056.060    ± 117.761  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4613.600     ± 94.814  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597791.668   ± 7007.677  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     610169.368   ± 3876.765  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     634322.755   ± 3240.428  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     644392.541   ± 2112.341  ops/s
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
