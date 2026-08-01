# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T06:44:35Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.52K | ± 82.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.23K | ± 226.19 | ops/s | 1.2x slower |
| prometheusAdd | 51.26K | ± 203.48 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.11K | ± 1.65K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 15.23 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.61K | ± 16.82 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 35.70 | ops/s | 11x slower |
| openTelemetryAdd | 1.53K | ± 390.27 | ops/s | 44x slower |
| openTelemetryInc | 1.29K | ± 62.02 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.14K | ± 61.43 | ops/s | 58x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 137.98 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 143.24 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 135.93 | ops/s | 1.7x slower |
| openTelemetryClassic | 687.26 | ± 38.40 | ops/s | 7.7x slower |
| openTelemetryExponential | 542.02 | ± 33.43 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 545.65K | ± 3.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.57K | ± 2.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.69K | ± 4.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 513.05K | ± 7.81K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49111.187   ± 1652.258  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1525.294    ± 390.275  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1288.430     ± 62.016  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1137.804     ± 61.429  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51264.415    ± 203.483  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66521.126     ± 82.673  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56230.885    ± 226.193  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6068.611     ± 35.699  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6692.375     ± 15.233  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6611.704     ± 16.823  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.258     ± 38.404  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        542.018     ± 33.428  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5278.204    ± 137.978  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.403    ± 135.933  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4324.482    ± 143.237  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513049.699   ± 7805.883  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521686.336   ± 4822.952  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540571.965   ± 2649.570  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     545651.448   ± 3767.271  ops/s
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
