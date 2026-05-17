# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-17T07:06:12Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.74K | ± 3.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 376.55 | ops/s | 1.1x slower |
| prometheusAdd | 47.60K | ± 997.43 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.97K | ± 1.80K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.27K | ± 26.95 | ops/s | 9.4x slower |
| simpleclientInc | 6.23K | ± 113.35 | ops/s | 9.4x slower |
| simpleclientAdd | 5.94K | ± 187.71 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.36K | ± 75.75 | ops/s | 43x slower |
| openTelemetryInc | 1.34K | ± 76.34 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.28K | ± 14.85 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.76K | ± 738.72 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 67.54 | ops/s | 1.1x slower |
| prometheusNative | 3.07K | ± 29.58 | ops/s | 1.6x slower |
| openTelemetryClassic | 611.45 | ± 20.47 | ops/s | 7.8x slower |
| openTelemetryExponential | 519.41 | ± 19.68 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 626.94K | ± 1.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 612.56K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 585.64K | ± 3.49K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 572.54K | ± 5.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42971.572   ± 1802.472  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1357.640     ± 75.752  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1342.794     ± 76.337  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1282.351     ± 14.847  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47600.829    ± 997.428  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58744.815   ± 3021.859  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51399.048    ± 376.555  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5939.742    ± 187.711  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6233.050    ± 113.349  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6274.050     ± 26.950  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.453     ± 20.470  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        519.406     ± 19.676  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4762.071    ± 738.722  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3070.869     ± 29.582  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4370.274     ± 67.536  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     572535.350   ± 5703.765  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     585640.620   ± 3492.711  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     612558.495   ± 3946.592  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     626939.175   ± 1738.230  ops/s
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
