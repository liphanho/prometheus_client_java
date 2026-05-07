# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-07T06:49:25Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.52K | ± 27.47 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.96K | ± 796.04 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.74K | ± 533.88 | ops/s | 1.1x slower |
| prometheusAdd | 28.33K | ± 114.39 | ops/s | 1.1x slower |
| simpleclientInc | 6.87K | ± 69.25 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.72K | ± 179.46 | ops/s | 4.7x slower |
| simpleclientAdd | 6.58K | ± 132.64 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.49K | ± 25.49 | ops/s | 21x slower |
| openTelemetryAdd | 1.44K | ± 73.04 | ops/s | 22x slower |
| openTelemetryInc | 1.43K | ± 16.65 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.36K | ± 41.48 | ops/s | **fastest** |
| prometheusClassic | 3.02K | ± 183.52 | ops/s | 1.4x slower |
| prometheusNative | 2.20K | ± 277.12 | ops/s | 2.0x slower |
| openTelemetryClassic | 521.79 | ± 11.15 | ops/s | 8.4x slower |
| openTelemetryExponential | 403.70 | ± 8.06 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.07K | ± 2.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 322.22K | ± 1.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 300.84K | ± 2.46K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.39K | ± 1.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28736.515    ± 533.882  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1436.565     ± 73.039  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.689     ± 16.650  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1486.094     ± 25.492  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28330.074    ± 114.387  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31517.509     ± 27.473  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30959.272    ± 796.035  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6582.953    ± 132.639  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6870.399     ± 69.254  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6720.066    ± 179.460  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.785     ± 11.154  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        403.698      ± 8.059  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3019.519    ± 183.522  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2200.473    ± 277.119  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4364.570     ± 41.480  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295388.420   ± 1978.882  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     300840.328   ± 2458.541  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     322216.438   ± 1800.762  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327066.861   ± 2281.952  ops/s
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
