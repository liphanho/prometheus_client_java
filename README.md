# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-01T07:44:30Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.15K | ± 106.77 | ops/s | **fastest** |
| prometheusInc | 26.37K | ± 72.56 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.30K | ± 213.14 | ops/s | 1.0x slower |
| prometheusAdd | 25.56K | ± 142.38 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.58K | ± 66.25 | ops/s | 4.1x slower |
| simpleclientInc | 6.54K | ± 29.51 | ops/s | 4.2x slower |
| simpleclientAdd | 6.32K | ± 47.99 | ops/s | 4.3x slower |
| openTelemetryIncNoLabels | 1.02K | ± 93.46 | ops/s | 27x slower |
| openTelemetryInc | 1.01K | ± 38.03 | ops/s | 27x slower |
| openTelemetryAdd | 977.98 | ± 118.96 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.26K | ± 33.95 | ops/s | **fastest** |
| prometheusClassic | 2.71K | ± 328.71 | ops/s | 1.6x slower |
| prometheusNative | 1.99K | ± 63.19 | ops/s | 2.1x slower |
| openTelemetryClassic | 393.27 | ± 25.55 | ops/s | 11x slower |
| openTelemetryExponential | 312.60 | ± 15.58 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 303.60K | ± 3.41K | ops/s | **fastest** |
| prometheusWriteToByteArray | 302.38K | ± 2.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 288.04K | ± 2.69K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 285.03K | ± 2.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27147.873    ± 106.767  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        977.977    ± 118.963  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1010.931     ± 38.029  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1021.000     ± 93.456  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25564.956    ± 142.382  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26371.733     ± 72.557  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26295.149    ± 213.136  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6324.992     ± 47.993  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6539.746     ± 29.511  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6578.985     ± 66.245  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        393.274     ± 25.551  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        312.601     ± 15.575  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2709.097    ± 328.715  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1994.322     ± 63.192  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4260.634     ± 33.951  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     285034.218   ± 2698.596  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     288037.069   ± 2687.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     302378.121   ± 2038.026  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     303602.890   ± 3406.476  ops/s
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
