# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-23T04:18:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.36K | ± 439.77 | ops/s | **fastest** |
| prometheusInc | 26.90K | ± 1.50K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.23K | ± 335.50 | ops/s | 1.0x slower |
| prometheusAdd | 25.64K | ± 103.48 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.63K | ± 69.42 | ops/s | 4.1x slower |
| simpleclientInc | 6.57K | ± 117.03 | ops/s | 4.2x slower |
| simpleclientAdd | 6.46K | ± 81.27 | ops/s | 4.2x slower |
| openTelemetryAdd | 1.11K | ± 27.20 | ops/s | 25x slower |
| openTelemetryInc | 1.10K | ± 75.43 | ops/s | 25x slower |
| openTelemetryIncNoLabels | 1.05K | ± 62.94 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.23K | ± 38.12 | ops/s | **fastest** |
| prometheusClassic | 2.66K | ± 123.68 | ops/s | 1.6x slower |
| prometheusNative | 1.99K | ± 25.41 | ops/s | 2.1x slower |
| openTelemetryClassic | 377.81 | ± 6.99 | ops/s | 11x slower |
| openTelemetryExponential | 316.41 | ± 5.33 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 305.21K | ± 1.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 301.67K | ± 2.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 284.27K | ± 1.48K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 281.34K | ± 1.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27355.758    ± 439.773  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1109.179     ± 27.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1103.043     ± 75.430  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1045.216     ± 62.939  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25640.371    ± 103.475  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26896.661   ± 1498.649  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26230.781    ± 335.503  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6461.254     ± 81.273  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6574.805    ± 117.032  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6634.415     ± 69.424  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        377.805      ± 6.991  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        316.410      ± 5.334  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2661.767    ± 123.676  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1994.307     ± 25.406  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4225.764     ± 38.124  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281337.700   ± 1040.373  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     284272.754   ± 1482.252  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     301665.819   ± 2037.236  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     305213.482   ± 1573.057  ops/s
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
