# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-19T06:39:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.75K | ± 1.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.33K | ± 487.73 | ops/s | 1.2x slower |
| prometheusAdd | 48.74K | ± 840.83 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.33K | ± 457.19 | ops/s | 1.3x slower |
| simpleclientInc | 6.25K | ± 129.31 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.16K | ± 200.92 | ops/s | 9.7x slower |
| simpleclientAdd | 5.64K | ± 146.71 | ops/s | 11x slower |
| openTelemetryInc | 1.40K | ± 75.29 | ops/s | 43x slower |
| openTelemetryAdd | 1.38K | ± 54.66 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.29K | ± 82.69 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 41.09 | ops/s | **fastest** |
| prometheusClassic | 4.40K | ± 909.55 | ops/s | 1.0x slower |
| prometheusNative | 3.05K | ± 142.60 | ops/s | 1.5x slower |
| openTelemetryClassic | 595.39 | ± 22.91 | ops/s | 7.7x slower |
| openTelemetryExponential | 498.33 | ± 14.56 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 638.81K | ± 7.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 617.93K | ± 20.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 612.98K | ± 5.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 598.08K | ± 7.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44327.419    ± 457.191  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1375.291     ± 54.658  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.483     ± 75.288  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1292.452     ± 82.692  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48741.078    ± 840.834  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59747.465   ± 1144.087  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51330.215    ± 487.726  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5639.875    ± 146.712  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6251.795    ± 129.309  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6156.508    ± 200.916  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.387     ± 22.915  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        498.334     ± 14.563  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4397.766    ± 909.552  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.574    ± 142.595  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4566.607     ± 41.087  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     598076.675   ± 7549.704  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     612984.625   ± 5747.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     617934.214  ± 20873.066  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     638806.097   ± 7316.048  ops/s
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
