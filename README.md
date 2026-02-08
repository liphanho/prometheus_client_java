# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-08T05:50:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.49K | ± 1.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.79K | ± 249.11 | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 622.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.58K | ± 241.47 | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 178.42 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.56K | ± 97.86 | ops/s | 10.0x slower |
| simpleclientAdd | 6.41K | ± 242.13 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 207.73 | ops/s | 46x slower |
| openTelemetryInc | 1.35K | ± 106.17 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.33K | ± 166.59 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 145.47 | ops/s | **fastest** |
| simpleclient | 4.57K | ± 26.56 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 16.87 | ops/s | 1.7x slower |
| openTelemetryClassic | 681.40 | ± 35.42 | ops/s | 7.9x slower |
| openTelemetryExponential | 576.95 | ± 48.55 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.76K | ± 5.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.00K | ± 4.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 511.19K | ± 2.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 510.92K | ± 2.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50578.751    ± 241.469  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1434.098    ± 207.734  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1345.405    ± 106.167  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1331.173    ± 166.594  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51237.901    ± 622.807  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65493.189   ± 1335.345  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56786.371    ± 249.108  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6410.617    ± 242.131  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6694.602    ± 178.423  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6561.304     ± 97.859  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.400     ± 35.425  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        576.945     ± 48.550  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5405.421    ± 145.474  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3118.928     ± 16.868  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4565.058     ± 26.555  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510920.613   ± 2507.788  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     511186.753   ± 2745.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526997.935   ± 4951.991  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539761.875   ± 5561.836  ops/s
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
