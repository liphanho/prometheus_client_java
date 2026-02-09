# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-09T05:44:36Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.16K | ± 342.89 | ops/s | **fastest** |
| prometheusInc | 30.76K | ± 1.27K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.74K | ± 568.07 | ops/s | 1.0x slower |
| prometheusAdd | 28.53K | ± 141.19 | ops/s | 1.1x slower |
| simpleclientInc | 7.04K | ± 53.12 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.82K | ± 226.28 | ops/s | 4.6x slower |
| simpleclientAdd | 6.63K | ± 149.05 | ops/s | 4.7x slower |
| openTelemetryAdd | 1.47K | ± 82.71 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 1.45K | ± 68.00 | ops/s | 21x slower |
| openTelemetryInc | 1.42K | ± 17.95 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.63K | ± 44.01 | ops/s | **fastest** |
| prometheusClassic | 3.29K | ± 294.09 | ops/s | 1.4x slower |
| prometheusNative | 2.26K | ± 153.12 | ops/s | 2.0x slower |
| openTelemetryClassic | 521.29 | ± 38.78 | ops/s | 8.9x slower |
| openTelemetryExponential | 399.96 | ± 16.26 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 337.69K | ± 2.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 335.21K | ± 2.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.00K | ± 1.08K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 309.99K | ± 925.64 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29742.760    ± 568.070  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1471.847     ± 82.710  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.626     ± 17.945  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1449.822     ± 67.998  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28533.989    ± 141.194  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30763.359   ± 1267.873  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31159.573    ± 342.891  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6633.244    ± 149.051  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7036.715     ± 53.120  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6823.475    ± 226.276  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        521.289     ± 38.780  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        399.961     ± 16.261  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3289.393    ± 294.093  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2260.634    ± 153.118  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4625.710     ± 44.009  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     309989.063    ± 925.640  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     311995.945   ± 1079.118  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     335214.649   ± 2520.502  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     337686.278   ± 2767.784  ops/s
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
