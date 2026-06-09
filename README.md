# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-09T07:27:03Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.40K | ± 25.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.90K | ± 176.52 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.88K | ± 1.43K | ops/s | 1.1x slower |
| prometheusAdd | 27.75K | ± 912.66 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.87K | ± 104.41 | ops/s | 4.6x slower |
| simpleclientInc | 6.86K | ± 121.64 | ops/s | 4.6x slower |
| simpleclientAdd | 6.59K | ± 96.41 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.48K | ± 118.30 | ops/s | 21x slower |
| openTelemetryAdd | 1.46K | ± 66.87 | ops/s | 21x slower |
| openTelemetryInc | 1.37K | ± 39.77 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 69.15 | ops/s | **fastest** |
| prometheusClassic | 2.97K | ± 151.03 | ops/s | 1.5x slower |
| prometheusNative | 2.29K | ± 227.80 | ops/s | 2.0x slower |
| openTelemetryClassic | 521.26 | ± 22.55 | ops/s | 8.7x slower |
| openTelemetryExponential | 407.85 | ± 24.03 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 270.08K | ± 4.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 269.23K | ± 2.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 251.46K | ± 1.62K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 250.16K | ± 1.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28882.068   ± 1425.587  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1463.051     ± 66.866  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1365.788     ± 39.766  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1479.789    ± 118.296  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27753.317    ± 912.660  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31399.801     ± 25.330  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30903.352    ± 176.517  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6591.399     ± 96.408  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6858.277    ± 121.638  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6873.653    ± 104.411  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.264     ± 22.555  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        407.853     ± 24.031  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2971.919    ± 151.026  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2289.468    ± 227.799  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4526.978     ± 69.151  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     250159.016   ± 1864.628  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     251459.568   ± 1621.487  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     269228.654   ± 2799.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     270076.571   ± 4266.384  ops/s
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
