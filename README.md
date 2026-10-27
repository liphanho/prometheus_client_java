# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-27T08:40:09Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.51K | ± 627.43 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.54K | ± 1.02K | ops/s | 1.0x slower |
| prometheusAdd | 59.66K | ± 319.29 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 51.88K | ± 12.50K | ops/s | 1.3x slower |
| simpleclientInc | 10.73K | ± 110.14 | ops/s | 6.3x slower |
| simpleclientAdd | 10.47K | ± 188.48 | ops/s | 6.4x slower |
| simpleclientNoLabelsInc | 10.39K | ± 386.42 | ops/s | 6.5x slower |
| openTelemetryInc | 1.96K | ± 408.98 | ops/s | 34x slower |
| openTelemetryAdd | 1.73K | ± 13.66 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.72K | ± 82.88 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.42K | ± 88.21 | ops/s | **fastest** |
| simpleclient | 6.91K | ± 73.91 | ops/s | 1.1x slower |
| prometheusNative | 5.07K | ± 455.01 | ops/s | 1.5x slower |
| openTelemetryClassic | 848.09 | ± 35.52 | ops/s | 8.7x slower |
| openTelemetryExponential | 718.00 | ± 22.62 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 771.21K | ± 33.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 728.45K | ± 17.12K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 725.61K | ± 7.60K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 715.81K | ± 14.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      51880.297  ± 12500.039  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1731.881     ± 13.656  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1963.831    ± 408.983  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1724.888     ± 82.883  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59657.558    ± 319.290  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67508.369    ± 627.434  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65542.559   ± 1018.862  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10467.669    ± 188.480  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10727.755    ± 110.143  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10388.600    ± 386.421  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        848.094     ± 35.523  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        717.996     ± 22.624  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7416.645     ± 88.212  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5070.134    ± 455.008  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6908.619     ± 73.907  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     725605.998   ± 7603.574  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     715806.776  ± 14318.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     728445.767  ± 17119.986  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     771205.878  ± 33789.556  ops/s
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
