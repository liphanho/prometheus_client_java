# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-07T07:41:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.53K | ± 3.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.43K | ± 635.01 | ops/s | 1.1x slower |
| prometheusAdd | 63.21K | ± 874.05 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.54K | ± 854.44 | ops/s | 1.3x slower |
| simpleclientInc | 8.01K | ± 208.37 | ops/s | 9.4x slower |
| simpleclientAdd | 7.94K | ± 55.51 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.88K | ± 315.63 | ops/s | 9.6x slower |
| openTelemetryAdd | 1.83K | ± 16.83 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.64K | ± 184.81 | ops/s | 46x slower |
| openTelemetryInc | 1.64K | ± 12.05 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.83K | ± 86.82 | ops/s | **fastest** |
| prometheusClassic | 5.68K | ± 13.40 | ops/s | 1.0x slower |
| prometheusNative | 3.99K | ± 174.03 | ops/s | 1.5x slower |
| openTelemetryClassic | 757.68 | ± 25.38 | ops/s | 7.7x slower |
| openTelemetryExponential | 700.27 | ± 40.74 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 775.92K | ± 6.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 744.62K | ± 8.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 737.94K | ± 2.82K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 717.55K | ± 2.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57542.008    ± 854.435  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1832.998     ± 16.832  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1637.642     ± 12.046  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1638.050    ± 184.808  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63206.983    ± 874.053  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75530.424   ± 3655.784  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66432.023    ± 635.013  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7938.934     ± 55.509  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8010.519    ± 208.375  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7883.932    ± 315.628  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        757.684     ± 25.375  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        700.269     ± 40.743  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5679.758     ± 13.400  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3986.147    ± 174.032  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5832.610     ± 86.823  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     717545.118   ± 2818.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     737939.038   ± 2819.813  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     744618.249   ± 8558.685  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     775916.175   ± 6019.544  ops/s
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
