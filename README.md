# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-11T05:27:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.10K | ± 258.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 193.55 | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 217.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.22K | ± 155.87 | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 56.54 | ops/s | 9.8x slower |
| simpleclientAdd | 6.41K | ± 147.99 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 68.20 | ops/s | 10x slower |
| openTelemetryInc | 1.50K | ± 138.26 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.34K | ± 223.40 | ops/s | 49x slower |
| openTelemetryAdd | 1.25K | ± 72.62 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.80K | ± 76.36 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 38.62 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 230.14 | ops/s | 1.9x slower |
| openTelemetryClassic | 706.82 | ± 57.75 | ops/s | 8.2x slower |
| openTelemetryExponential | 528.16 | ± 30.82 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 542.42K | ± 7.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.17K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.54K | ± 2.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.34K | ± 6.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50223.036    ± 155.874  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1248.897     ± 72.619  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1498.232    ± 138.257  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1344.794    ± 223.400  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51472.533    ± 217.177  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66097.257    ± 258.175  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57206.004    ± 193.549  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6412.349    ± 147.990  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6746.859     ± 56.540  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6360.244     ± 68.203  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        706.818     ± 57.746  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        528.164     ± 30.823  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5798.212     ± 76.358  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3074.800    ± 230.140  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.882     ± 38.621  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515335.760   ± 6794.378  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519542.866   ± 2436.295  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531170.129   ± 3079.966  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542420.867   ± 7174.219  ops/s
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
