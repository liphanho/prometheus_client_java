# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-15T04:08:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.22K | ± 1.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 284.77 | ops/s | 1.1x slower |
| prometheusAdd | 49.74K | ± 1.85K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.93K | ± 919.93 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 63.10 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.52K | ± 143.58 | ops/s | 9.9x slower |
| simpleclientAdd | 6.47K | ± 8.76 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.41K | ± 152.69 | ops/s | 45x slower |
| openTelemetryAdd | 1.37K | ± 206.51 | ops/s | 47x slower |
| openTelemetryInc | 1.28K | ± 31.88 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 105.77 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 39.09 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 14.77 | ops/s | 1.7x slower |
| openTelemetryClassic | 678.64 | ± 26.17 | ops/s | 7.9x slower |
| openTelemetryExponential | 550.82 | ± 33.89 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.97K | ± 5.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 508.22K | ± 5.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.31K | ± 5.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.78K | ± 1.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48930.433    ± 919.927  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1367.759    ± 206.506  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.153     ± 31.885  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1412.272    ± 152.686  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49736.742   ± 1845.499  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64219.515   ± 1755.246  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56586.678    ± 284.773  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6465.351      ± 8.762  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6659.251     ± 63.099  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6517.347    ± 143.585  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.645     ± 26.172  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.817     ± 33.886  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5357.449    ± 105.769  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3126.485     ± 14.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4427.024     ± 39.086  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499776.119   ± 1929.190  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507313.631   ± 5294.043  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     508221.760   ± 5695.402  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511970.900   ± 5199.506  ops/s
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
