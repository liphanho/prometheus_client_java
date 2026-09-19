# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-19T08:22:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.54K | ± 391.80 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 358.14 | ops/s | 1.2x slower |
| prometheusAdd | 51.59K | ± 164.19 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.57K | ± 301.78 | ops/s | 1.4x slower |
| simpleclientInc | 6.45K | ± 196.50 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 201.44 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 160.14 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 216.68 | ops/s | 43x slower |
| openTelemetryInc | 1.29K | ± 34.92 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.22K | ± 17.13 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 34.81 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 43.24 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 121.56 | ops/s | 1.7x slower |
| openTelemetryClassic | 685.78 | ± 39.67 | ops/s | 7.6x slower |
| openTelemetryExponential | 571.43 | ± 19.01 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 545.20K | ± 5.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 537.85K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.52K | ± 5.36K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 513.84K | ± 5.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47574.799    ± 301.779  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1509.154    ± 216.678  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1289.512     ± 34.923  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1216.385     ± 17.131  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51589.295    ± 164.187  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65542.813    ± 391.800  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56830.162    ± 358.137  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6214.614    ± 160.137  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6447.449    ± 196.498  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6359.131    ± 201.436  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.780     ± 39.670  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.434     ± 19.010  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5238.045     ± 34.809  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3030.381    ± 121.556  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4472.776     ± 43.239  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513842.826   ± 5157.479  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514521.172   ± 5355.061  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     537853.177   ± 3060.572  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     545197.542   ± 5059.902  ops/s
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
