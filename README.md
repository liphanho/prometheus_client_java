# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-02T06:45:00Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.16K | ± 1.03K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.94K | ± 65.33 | ops/s | 1.2x slower |
| prometheusAdd | 48.52K | ± 1.01K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.53K | ± 362.22 | ops/s | 1.3x slower |
| simpleclientInc | 6.23K | ± 107.75 | ops/s | 9.5x slower |
| simpleclientAdd | 6.02K | ± 180.85 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.01K | ± 186.14 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.41K | ± 118.13 | ops/s | 42x slower |
| openTelemetryAdd | 1.38K | ± 89.90 | ops/s | 43x slower |
| openTelemetryInc | 1.29K | ± 77.50 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.99K | ± 779.79 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 34.96 | ops/s | 1.1x slower |
| prometheusNative | 3.07K | ± 88.73 | ops/s | 1.6x slower |
| openTelemetryClassic | 594.05 | ± 21.75 | ops/s | 8.4x slower |
| openTelemetryExponential | 534.00 | ± 11.88 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 623.97K | ± 4.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.97K | ± 2.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 595.40K | ± 3.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 576.09K | ± 3.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44531.616    ± 362.217  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1375.046     ± 89.898  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1291.768     ± 77.500  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1409.301    ± 118.128  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48519.044   ± 1011.592  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59164.529   ± 1033.064  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50939.337     ± 65.330  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6023.793    ± 180.852  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6226.060    ± 107.749  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6010.127    ± 186.141  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        594.050     ± 21.746  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.000     ± 11.883  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4993.383    ± 779.792  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.857     ± 88.731  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4411.264     ± 34.960  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     576091.740   ± 3120.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     595400.762   ± 3640.806  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609972.343   ± 2621.041  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     623970.511   ± 4718.294  ops/s
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
