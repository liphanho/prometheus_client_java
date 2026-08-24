# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T04:19:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.45K | ± 50.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.25K | ± 999.03 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.16K | ± 1.26K | ops/s | 1.1x slower |
| prometheusAdd | 28.37K | ± 25.57 | ops/s | 1.1x slower |
| simpleclientInc | 6.91K | ± 108.12 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.74K | ± 172.52 | ops/s | 4.7x slower |
| simpleclientAdd | 6.70K | ± 49.51 | ops/s | 4.7x slower |
| openTelemetryAdd | 1.41K | ± 54.78 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.40K | ± 86.66 | ops/s | 23x slower |
| openTelemetryInc | 1.35K | ± 70.23 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 43.86 | ops/s | **fastest** |
| prometheusClassic | 3.20K | ± 86.54 | ops/s | 1.4x slower |
| prometheusNative | 2.08K | ± 20.15 | ops/s | 2.2x slower |
| openTelemetryClassic | 531.12 | ± 10.89 | ops/s | 8.5x slower |
| openTelemetryExponential | 408.40 | ± 6.60 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.10K | ± 2.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 324.96K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.27K | ± 2.67K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 293.53K | ± 2.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29155.876   ± 1264.791  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1408.515     ± 54.777  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1345.430     ± 70.231  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1397.568     ± 86.657  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28367.214     ± 25.572  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31451.500     ± 50.262  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30254.083    ± 999.032  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6699.541     ± 49.515  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6911.219    ± 108.122  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6735.314    ± 172.523  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        531.119     ± 10.892  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        408.402      ± 6.596  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3197.655     ± 86.536  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2075.035     ± 20.149  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4506.026     ± 43.859  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293528.587   ± 2853.152  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299266.953   ± 2674.511  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     324959.170   ± 3233.302  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327104.959   ± 2311.900  ops/s
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
