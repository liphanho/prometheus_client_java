# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-27T05:51:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.30K | ± 1.51K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.32K | ± 992.68 | ops/s | 1.2x slower |
| prometheusAdd | 50.94K | ± 656.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.01K | ± 1.08K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 21.89 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.33K | ± 108.83 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 299.72 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.32K | ± 160.09 | ops/s | 50x slower |
| openTelemetryInc | 1.28K | ± 5.60 | ops/s | 51x slower |
| openTelemetryAdd | 1.25K | ± 13.58 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 23.19 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 63.66 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 141.54 | ops/s | 1.7x slower |
| openTelemetryClassic | 691.28 | ± 9.74 | ops/s | 7.6x slower |
| openTelemetryExponential | 593.30 | ± 12.54 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 531.55K | ± 4.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.39K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.11K | ± 8.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.84K | ± 4.71K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49011.368   ± 1079.820  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1247.491     ± 13.575  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1280.245      ± 5.596  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1317.637    ± 160.092  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50939.869    ± 656.096  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65297.948   ± 1514.865  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56324.114    ± 992.677  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6126.335    ± 299.719  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.055     ± 21.886  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6326.583    ± 108.832  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.275      ± 9.737  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        593.305     ± 12.539  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5286.854     ± 23.185  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3057.293    ± 141.543  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4437.069     ± 63.659  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506842.694   ± 4712.851  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515113.469   ± 8313.042  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527388.550   ± 2602.115  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531547.649   ± 4584.412  ops/s
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
