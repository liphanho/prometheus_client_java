# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-10T05:48:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.41K | ± 263.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 450.90 | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 267.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.71K | ± 657.69 | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 109.59 | ops/s | 9.9x slower |
| simpleclientAdd | 6.56K | ± 27.75 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 213.97 | ops/s | 10x slower |
| openTelemetryAdd | 1.86K | ± 94.45 | ops/s | 36x slower |
| openTelemetryIncNoLabels | 1.37K | ± 178.66 | ops/s | 48x slower |
| openTelemetryInc | 1.22K | ± 15.22 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 121.68 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 18.03 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 228.08 | ops/s | 1.8x slower |
| openTelemetryClassic | 668.96 | ± 14.52 | ops/s | 7.9x slower |
| openTelemetryExponential | 572.45 | ± 36.50 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 549.70K | ± 6.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.14K | ± 9.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.51K | ± 10.13K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 516.90K | ± 2.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47706.044    ± 657.685  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1858.516     ± 94.455  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1218.620     ± 15.222  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1371.417    ± 178.657  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51546.097    ± 267.497  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66410.703    ± 263.345  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56912.118    ± 450.904  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6556.588     ± 27.755  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6682.118    ± 109.591  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6425.814    ± 213.970  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.960     ± 14.519  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.451     ± 36.496  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5304.672    ± 121.677  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.636    ± 228.078  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4515.695     ± 18.030  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516896.092   ± 2067.674  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522509.332  ± 10127.332  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539143.276   ± 9583.742  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549698.125   ± 6892.380  ops/s
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
