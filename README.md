# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-21T10:33:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 30.73K | ± 646.80 | ops/s | **fastest** |
| prometheusInc | 30.28K | ± 120.09 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.14K | ± 246.41 | ops/s | 1.0x slower |
| prometheusAdd | 29.33K | ± 252.54 | ops/s | 1.0x slower |
| simpleclientInc | 7.46K | ± 60.68 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 7.35K | ± 107.70 | ops/s | 4.2x slower |
| simpleclientAdd | 7.20K | ± 104.89 | ops/s | 4.3x slower |
| openTelemetryInc | 1.13K | ± 65.64 | ops/s | 27x slower |
| openTelemetryAdd | 1.11K | ± 106.24 | ops/s | 28x slower |
| openTelemetryIncNoLabels | 1.09K | ± 47.46 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.69K | ± 95.25 | ops/s | **fastest** |
| prometheusClassic | 3.15K | ± 405.38 | ops/s | 1.5x slower |
| prometheusNative | 2.19K | ± 32.20 | ops/s | 2.1x slower |
| openTelemetryClassic | 469.52 | ± 20.51 | ops/s | 10.0x slower |
| openTelemetryExponential | 399.66 | ± 15.06 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 285.79K | ± 11.01K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 264.09K | ± 15.03K | ops/s | 1.1x slower |
| prometheusWriteToByteArray | 256.74K | ± 1.11K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 255.41K | ± 14.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30725.155    ± 646.803  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1113.408    ± 106.236  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1131.099     ± 65.636  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1085.572     ± 47.463  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29333.771    ± 252.537  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30278.058    ± 120.090  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30139.650    ± 246.414  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7201.329    ± 104.893  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7463.572     ± 60.676  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7345.644    ± 107.698  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        469.515     ± 20.506  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        399.657     ± 15.058  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3150.435    ± 405.378  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2189.755     ± 32.203  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4689.355     ± 95.254  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     264088.884  ± 15027.382  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     255408.728  ± 14271.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     256735.405   ± 1112.236  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     285791.444  ± 11006.928  ops/s
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
