# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-21T08:08:39Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.10K | ± 2.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.44K | ± 1.41K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.30K | ± 803.06 | ops/s | 1.3x slower |
| prometheusAdd | 38.69K | ± 13.66K | ops/s | 1.5x slower |
| simpleclientInc | 6.21K | ± 112.46 | ops/s | 9.4x slower |
| simpleclientAdd | 6.07K | ± 187.82 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.98K | ± 199.32 | ops/s | 9.7x slower |
| openTelemetryInc | 1.44K | ± 216.81 | ops/s | 40x slower |
| openTelemetryAdd | 1.41K | ± 123.63 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.34K | ± 44.03 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.38K | ± 187.38 | ops/s | **fastest** |
| simpleclient | 4.33K | ± 84.38 | ops/s | 1.2x slower |
| prometheusNative | 2.99K | ± 96.35 | ops/s | 1.8x slower |
| openTelemetryClassic | 609.22 | ± 9.42 | ops/s | 8.8x slower |
| openTelemetryExponential | 533.40 | ± 8.39 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.98K | ± 5.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 639.53K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 615.19K | ± 6.41K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 607.80K | ± 4.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44296.523    ± 803.060  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1406.483    ± 123.635  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1437.954    ± 216.807  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1338.879     ± 44.026  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      38688.638  ± 13656.612  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58099.452   ± 2216.995  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50443.488   ± 1413.854  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6069.765    ± 187.822  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6209.860    ± 112.463  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5976.169    ± 199.319  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        609.222      ± 9.423  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.396      ± 8.393  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5376.512    ± 187.382  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2992.900     ± 96.351  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4330.158     ± 84.378  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     607798.151   ± 4846.545  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     615185.156   ± 6414.655  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     639531.007   ± 3063.154  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643978.895   ± 5002.914  ops/s
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
