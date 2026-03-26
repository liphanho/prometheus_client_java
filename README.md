# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-26T05:50:42Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.50K | ± 1.14K | ops/s | **fastest** |
| prometheusInc | 30.39K | ± 1.03K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.72K | ± 1.02K | ops/s | 1.0x slower |
| prometheusAdd | 28.55K | ± 149.83 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.96K | ± 185.54 | ops/s | 4.4x slower |
| simpleclientInc | 6.95K | ± 101.52 | ops/s | 4.4x slower |
| simpleclientAdd | 6.81K | ± 52.31 | ops/s | 4.5x slower |
| openTelemetryAdd | 1.46K | ± 82.00 | ops/s | 21x slower |
| openTelemetryInc | 1.45K | ± 42.58 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 1.36K | ± 117.72 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 16.65 | ops/s | **fastest** |
| prometheusClassic | 2.98K | ± 167.84 | ops/s | 1.5x slower |
| prometheusNative | 2.12K | ± 248.63 | ops/s | 2.1x slower |
| openTelemetryClassic | 503.77 | ± 33.59 | ops/s | 9.0x slower |
| openTelemetryExponential | 404.48 | ± 10.06 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 325.01K | ± 2.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 323.52K | ± 4.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.54K | ± 3.01K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.51K | ± 2.87K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29722.107   ± 1021.510  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1461.745     ± 81.999  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1452.317     ± 42.585  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1360.342    ± 117.717  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28550.356    ± 149.833  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30389.392   ± 1028.249  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30495.588   ± 1138.085  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6813.575     ± 52.309  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6953.384    ± 101.516  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6957.299    ± 185.541  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        503.769     ± 33.589  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.478     ± 10.057  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2984.514    ± 167.842  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2115.644    ± 248.628  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4530.527     ± 16.654  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298507.128   ± 2870.042  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301537.970   ± 3007.415  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     323517.051   ± 4071.337  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     325006.881   ± 2653.950  ops/s
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
