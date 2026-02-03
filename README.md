# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-03T05:32:54Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.58K | ± 43.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.31K | ± 1.06K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.47K | ± 1.23K | ops/s | 1.1x slower |
| prometheusAdd | 28.43K | ± 59.89 | ops/s | 1.1x slower |
| simpleclientInc | 7.14K | ± 95.56 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.91K | ± 278.71 | ops/s | 4.6x slower |
| simpleclientAdd | 6.65K | ± 140.64 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.43K | ± 33.95 | ops/s | 22x slower |
| openTelemetryInc | 1.43K | ± 137.75 | ops/s | 22x slower |
| openTelemetryAdd | 1.38K | ± 99.89 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 23.68 | ops/s | **fastest** |
| prometheusClassic | 3.16K | ± 210.51 | ops/s | 1.4x slower |
| prometheusNative | 2.18K | ± 161.71 | ops/s | 2.1x slower |
| openTelemetryClassic | 524.52 | ± 36.60 | ops/s | 8.7x slower |
| openTelemetryExponential | 395.63 | ± 21.44 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 337.42K | ± 1.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 331.90K | ± 2.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.45K | ± 866.19 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 308.83K | ± 1.95K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29471.648   ± 1234.729  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1380.048     ± 99.892  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1427.332    ± 137.754  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1432.946     ± 33.951  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28434.355     ± 59.886  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31577.983     ± 43.277  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30311.964   ± 1055.817  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6648.485    ± 140.640  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7137.524     ± 95.557  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6910.102    ± 278.708  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        524.518     ± 36.602  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        395.628     ± 21.438  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3162.481    ± 210.513  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2182.820    ± 161.705  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4538.080     ± 23.680  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     308833.574   ± 1951.239  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     312452.859    ± 866.187  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     331904.619   ± 2479.922  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     337417.395   ± 1810.619  ops/s
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
