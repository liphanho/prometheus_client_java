# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-27T07:38:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.12K | ± 419.44 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 272.39 | ops/s | 1.2x slower |
| prometheusAdd | 49.02K | ± 4.03K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.65K | ± 7.96K | ops/s | 1.5x slower |
| simpleclientInc | 6.66K | ± 76.52 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.51K | ± 135.64 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 188.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 215.40 | ops/s | 44x slower |
| openTelemetryInc | 1.37K | ± 179.49 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.20K | ± 54.97 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 19.70 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 43.87 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 49.42 | ops/s | 1.7x slower |
| openTelemetryClassic | 678.62 | ± 22.75 | ops/s | 7.8x slower |
| openTelemetryExponential | 564.74 | ± 35.12 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.87K | ± 8.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 522.22K | ± 8.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.71K | ± 2.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 501.06K | ± 4.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44654.793   ± 7963.020  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1513.074    ± 215.399  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.069    ± 179.491  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1199.859     ± 54.973  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49021.840   ± 4033.484  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66120.542    ± 419.435  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56747.410    ± 272.388  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6134.440    ± 188.847  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6659.110     ± 76.525  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6509.110    ± 135.637  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.615     ± 22.748  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.745     ± 35.122  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5263.941     ± 19.705  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3154.479     ± 49.416  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.468     ± 43.870  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501055.268   ± 4676.390  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512712.486   ± 2764.568  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     522219.507   ± 8464.886  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532865.998   ± 8955.485  ops/s
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
