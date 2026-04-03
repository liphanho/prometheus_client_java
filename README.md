# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-03T05:47:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.26K | ± 235.07 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 382.72 | ops/s | 1.2x slower |
| prometheusAdd | 51.42K | ± 282.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.31K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 170.83 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 174.67 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 318.67 | ops/s | 11x slower |
| openTelemetryAdd | 1.36K | ± 115.23 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.32K | ± 121.50 | ops/s | 50x slower |
| openTelemetryInc | 1.21K | ± 55.46 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 127.22 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 25.98 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 143.02 | ops/s | 1.9x slower |
| openTelemetryClassic | 696.38 | ± 28.98 | ops/s | 8.1x slower |
| openTelemetryExponential | 564.38 | ± 37.81 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 530.59K | ± 3.18K | ops/s | **fastest** |
| prometheusWriteToNull | 529.48K | ± 6.76K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.62K | ± 9.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.59K | ± 4.01K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49417.358   ± 1312.860  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1361.937    ± 115.226  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1213.320     ± 55.465  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1319.924    ± 121.496  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51415.113    ± 282.311  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66256.419    ± 235.069  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57036.126    ± 382.722  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6129.651    ± 318.667  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6566.613    ± 170.831  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6399.312    ± 174.668  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.383     ± 28.978  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.381     ± 37.809  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5613.956    ± 127.218  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.345    ± 143.016  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4493.769     ± 25.978  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508588.299   ± 4013.490  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509620.675   ± 9613.467  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530585.621   ± 3176.343  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529476.828   ± 6762.153  ops/s
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
