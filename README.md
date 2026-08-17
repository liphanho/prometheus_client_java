# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-17T04:16:31Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.19K | ± 361.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.04K | ± 908.02 | ops/s | 1.2x slower |
| prometheusAdd | 51.68K | ± 137.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.22K | ± 748.99 | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 167.39 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 146.56 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 27.84 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 248.24 | ops/s | 47x slower |
| openTelemetryInc | 1.33K | ± 135.93 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.18K | ± 65.30 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 342.74 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 67.84 | ops/s | 1.2x slower |
| prometheusNative | 3.22K | ± 58.96 | ops/s | 1.6x slower |
| openTelemetryClassic | 661.50 | ± 29.50 | ops/s | 7.9x slower |
| openTelemetryExponential | 562.04 | ± 31.73 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.93K | ± 7.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 534.42K | ± 6.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 511.70K | ± 4.80K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 509.46K | ± 3.88K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48216.272    ± 748.990  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1398.882    ± 248.241  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.447    ± 135.929  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1181.112     ± 65.297  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51677.005    ± 137.025  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66190.439    ± 361.007  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56036.413    ± 908.016  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6457.854     ± 27.844  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6602.700    ± 167.388  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6515.310    ± 146.558  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.497     ± 29.497  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.043     ± 31.728  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5239.178    ± 342.745  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3216.571     ± 58.958  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4428.879     ± 67.843  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511697.764   ± 4801.966  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509462.835   ± 3875.284  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534419.742   ± 6901.856  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541925.442   ± 7267.644  ops/s
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
