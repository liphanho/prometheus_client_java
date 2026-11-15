# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-15T10:09:34Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.54K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 452.74 | ops/s | 1.1x slower |
| prometheusAdd | 51.00K | ± 406.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.36K | ± 1.38K | ops/s | 1.3x slower |
| simpleclientInc | 6.49K | ± 141.83 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 167.45 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 193.47 | ops/s | 11x slower |
| openTelemetryAdd | 1.39K | ± 204.75 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 16.51 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.24K | ± 28.89 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 140.36 | ops/s | **fastest** |
| simpleclient | 4.33K | ± 19.84 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 169.23 | ops/s | 1.7x slower |
| openTelemetryClassic | 758.82 | ± 8.53 | ops/s | 6.9x slower |
| openTelemetryExponential | 579.51 | ± 24.94 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 484.67K | ± 4.47K | ops/s | **fastest** |
| prometheusWriteToNull | 482.53K | ± 8.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 462.42K | ± 11.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.48K | ± 5.88K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49358.786   ± 1376.246  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1394.240    ± 204.745  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1262.084     ± 16.513  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1243.981     ± 28.888  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51000.627    ± 406.865  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64537.124   ± 1388.341  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56380.882    ± 452.739  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6124.193    ± 193.465  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6488.616    ± 141.834  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6384.472    ± 167.451  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        758.819      ± 8.531  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.511     ± 24.944  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5248.653    ± 140.357  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3079.868    ± 169.231  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4328.035     ± 19.842  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459480.726   ± 5878.426  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     462419.087  ± 11905.634  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484673.931   ± 4470.159  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482532.673   ± 8438.534  ops/s
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
