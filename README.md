# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-20T07:38:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.52K | ± 898.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.61K | ± 277.15 | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 254.20 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.62K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 64.02 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 174.31 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 245.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 236.41 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.38K | ± 203.07 | ops/s | 47x slower |
| openTelemetryInc | 1.37K | ± 195.60 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.02K | ± 16.72 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 17.77 | ops/s | 1.1x slower |
| prometheusNative | 3.00K | ± 172.13 | ops/s | 1.7x slower |
| openTelemetryClassic | 661.96 | ± 9.41 | ops/s | 7.6x slower |
| openTelemetryExponential | 559.65 | ± 36.35 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.78K | ± 3.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 515.04K | ± 7.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 502.10K | ± 2.71K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 500.86K | ± 4.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48622.531   ± 1329.454  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1420.463    ± 236.405  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.196    ± 195.595  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1383.341    ± 203.071  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51471.601    ± 254.202  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65524.156    ± 898.635  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56610.643    ± 277.150  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6179.226    ± 245.850  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6610.179     ± 64.017  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.676    ± 174.312  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.963      ± 9.412  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.648     ± 36.351  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5019.506     ± 16.719  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3002.223    ± 172.127  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.138     ± 17.767  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     502103.428   ± 2709.322  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     500858.791   ± 4172.418  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515036.235   ± 7442.709  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529778.353   ± 3110.771  ops/s
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
