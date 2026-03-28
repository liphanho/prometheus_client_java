# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-28T05:39:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.39K | ± 333.44 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.36K | ± 936.49 | ops/s | 1.2x slower |
| prometheusAdd | 51.63K | ± 227.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.28K | ± 1.55K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.62K | ± 19.21 | ops/s | 10x slower |
| simpleclientInc | 6.57K | ± 220.22 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 356.65 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.29K | ± 84.16 | ops/s | 52x slower |
| openTelemetryAdd | 1.25K | ± 29.92 | ops/s | 53x slower |
| openTelemetryInc | 1.21K | ± 25.71 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 105.34 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 43.92 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 78.92 | ops/s | 1.7x slower |
| openTelemetryClassic | 679.81 | ± 16.88 | ops/s | 7.8x slower |
| openTelemetryExponential | 559.15 | ± 29.12 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.02K | ± 4.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.22K | ± 4.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.53K | ± 10.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 512.04K | ± 4.39K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49282.842   ± 1546.389  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1248.338     ± 29.923  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1211.220     ± 25.711  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1286.669     ± 84.164  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51632.701    ± 227.882  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66392.268    ± 333.440  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55364.456    ± 936.491  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6115.050    ± 356.650  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6565.423    ± 220.217  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6623.060     ± 19.209  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.810     ± 16.875  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.151     ± 29.118  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5286.820    ± 105.342  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3164.500     ± 78.923  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.923     ± 43.921  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     512040.040   ± 4390.594  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520532.804  ± 10725.180  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529223.543   ± 4055.423  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537021.378   ± 4787.579  ops/s
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
