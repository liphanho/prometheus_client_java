# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T08:24:40Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.77K | ± 2.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 963.84 | ops/s | 1.1x slower |
| prometheusAdd | 48.53K | ± 993.24 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.36K | ± 661.50 | ops/s | 1.3x slower |
| simpleclientInc | 6.12K | ± 206.90 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.01K | ± 204.21 | ops/s | 9.4x slower |
| simpleclientAdd | 5.94K | ± 188.31 | ops/s | 9.6x slower |
| openTelemetryAdd | 1.46K | ± 113.15 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.43K | ± 63.37 | ops/s | 40x slower |
| openTelemetryInc | 1.31K | ± 20.89 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.56K | ± 93.75 | ops/s | **fastest** |
| simpleclient | 4.58K | ± 80.26 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 95.57 | ops/s | 1.8x slower |
| openTelemetryClassic | 638.00 | ± 2.13 | ops/s | 8.7x slower |
| openTelemetryExponential | 546.03 | ± 25.90 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 621.26K | ± 11.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.33K | ± 3.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 588.60K | ± 4.18K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 578.14K | ± 5.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44358.103    ± 661.495  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1458.707    ± 113.155  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1313.242     ± 20.894  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1427.703     ± 63.373  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48530.476    ± 993.238  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56772.161   ± 2574.840  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51404.527    ± 963.838  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5940.015    ± 188.306  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6116.209    ± 206.897  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6007.859    ± 204.209  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        638.000      ± 2.127  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.030     ± 25.904  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5558.521     ± 93.753  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3156.635     ± 95.572  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4582.732     ± 80.258  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     578137.658   ± 5248.671  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     588596.087   ± 4175.636  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609326.453   ± 3591.878  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     621262.090  ± 11350.113  ops/s
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
