# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-29T09:13:47Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.62K | ± 815.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.15K | ± 1.33K | ops/s | 1.2x slower |
| prometheusAdd | 51.62K | ± 73.74 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.08K | ± 7.94K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.60K | ± 12.96 | ops/s | 9.9x slower |
| simpleclientInc | 6.42K | ± 94.59 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 214.35 | ops/s | 11x slower |
| openTelemetryAdd | 1.38K | ± 208.70 | ops/s | 48x slower |
| openTelemetryInc | 1.32K | ± 133.89 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.20K | ± 24.85 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 111.76 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 52.36 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 132.83 | ops/s | 1.7x slower |
| openTelemetryClassic | 665.04 | ± 17.31 | ops/s | 7.9x slower |
| openTelemetryExponential | 573.26 | ± 41.03 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.34K | ± 5.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.41K | ± 5.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.09K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.10K | ± 3.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44080.302   ± 7936.390  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1379.381    ± 208.696  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1322.913    ± 133.890  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1197.982     ± 24.851  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51619.929     ± 73.739  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65618.629    ± 815.522  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56147.610   ± 1330.799  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6151.467    ± 214.349  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6417.826     ± 94.588  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6602.081     ± 12.960  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.037     ± 17.307  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.262     ± 41.032  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5279.271    ± 111.758  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3088.471    ± 132.828  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.655     ± 52.360  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495104.218   ± 3293.338  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505094.738   ± 5821.850  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512407.715   ± 5880.296  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526343.031   ± 5209.104  ops/s
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
