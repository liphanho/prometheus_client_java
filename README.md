# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T04:16:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 62.77K | ± 4.74K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.87K | ± 311.70 | ops/s | 1.1x slower |
| prometheusAdd | 51.58K | ± 116.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.55K | ± 737.04 | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 121.03 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.48K | ± 177.89 | ops/s | 9.7x slower |
| simpleclientAdd | 6.29K | ± 262.09 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 1.48K | ± 210.83 | ops/s | 42x slower |
| openTelemetryAdd | 1.44K | ± 281.10 | ops/s | 44x slower |
| openTelemetryInc | 1.31K | ± 29.58 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 236.13 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 22.91 | ops/s | 1.2x slower |
| prometheusNative | 2.87K | ± 113.16 | ops/s | 1.8x slower |
| openTelemetryClassic | 651.07 | ± 17.23 | ops/s | 7.9x slower |
| openTelemetryExponential | 570.20 | ± 29.17 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.33K | ± 2.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 535.02K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.32K | ± 3.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 513.00K | ± 2.14K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48547.351    ± 737.035  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1435.472    ± 281.097  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1306.069     ± 29.579  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1483.081    ± 210.827  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51580.623    ± 116.333  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      62774.038   ± 4737.939  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54871.328    ± 311.699  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6288.300    ± 262.087  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6621.979    ± 121.030  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.256    ± 177.893  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.066     ± 17.232  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.204     ± 29.167  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5158.666    ± 236.134  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2865.577    ± 113.162  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.169     ± 22.907  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513003.129   ± 2143.689  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522324.354   ± 3970.560  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     535023.472   ± 5270.671  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538330.563   ± 2355.400  ops/s
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
