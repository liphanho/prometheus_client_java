# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T08:58:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.01K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.09K | ± 3.37K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.71K | ± 2.43K | ops/s | 1.3x slower |
| prometheusAdd | 47.70K | ± 5.05K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 60.26 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.37K | ± 195.27 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 222.71 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.28K | ± 162.17 | ops/s | 51x slower |
| openTelemetryInc | 1.28K | ± 69.69 | ops/s | 51x slower |
| openTelemetryAdd | 1.25K | ± 55.46 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 229.74 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 71.96 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 45.90 | ops/s | 1.7x slower |
| openTelemetryClassic | 677.47 | ± 21.84 | ops/s | 8.1x slower |
| openTelemetryExponential | 571.04 | ± 30.19 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 542.79K | ± 11.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.12K | ± 10.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.76K | ± 6.99K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 508.48K | ± 5.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49710.340   ± 2433.842  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1246.357     ± 55.463  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.902     ± 69.686  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1284.871    ± 162.167  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47696.662   ± 5046.042  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65013.621   ± 1229.052  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55094.795   ± 3373.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6343.264    ± 222.708  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.898     ± 60.259  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6370.918    ± 195.270  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.466     ± 21.837  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.037     ± 30.187  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5469.626    ± 229.742  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3127.486     ± 45.896  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4411.670     ± 71.959  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508479.618   ± 5495.039  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516759.886   ± 6993.205  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517120.232  ± 10648.002  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542792.816  ± 11488.714  ops/s
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
