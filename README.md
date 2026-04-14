# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-14T06:02:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.47K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.04K | ± 816.82 | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 277.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.61K | ± 1.19K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 25.58 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.50K | ± 189.66 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 252.62 | ops/s | 11x slower |
| openTelemetryInc | 1.48K | ± 173.66 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.43K | ± 233.41 | ops/s | 46x slower |
| openTelemetryAdd | 1.28K | ± 41.00 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.38K | ± 262.84 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 22.80 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 110.26 | ops/s | 1.7x slower |
| openTelemetryClassic | 688.03 | ± 50.98 | ops/s | 7.8x slower |
| openTelemetryExponential | 574.90 | ± 9.56 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 528.97K | ± 2.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.81K | ± 9.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.55K | ± 2.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.26K | ± 12.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48611.065   ± 1187.764  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1280.213     ± 40.997  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1481.843    ± 173.658  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1425.993    ± 233.407  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51243.412    ± 277.169  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65465.185   ± 1576.766  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56041.749    ± 816.825  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6106.159    ± 252.617  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.245     ± 25.579  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6496.434    ± 189.658  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.030     ± 50.976  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.904      ± 9.565  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5380.238    ± 262.845  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3098.210    ± 110.259  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4433.458     ± 22.798  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486258.038  ± 12735.796  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508554.751   ± 2487.697  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521805.017   ± 9801.896  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528970.312   ± 2766.349  ops/s
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
