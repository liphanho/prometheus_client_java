# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-02T07:59:15Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 424.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.29K | ± 1.37K | ops/s | 1.2x slower |
| prometheusAdd | 50.48K | ± 1.64K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.04K | ± 838.46 | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 86.60 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.42K | ± 149.37 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 193.20 | ops/s | 10x slower |
| openTelemetryAdd | 1.25K | ± 38.47 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.24K | ± 52.84 | ops/s | 53x slower |
| openTelemetryInc | 1.23K | ± 4.49 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 170.38 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 66.79 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 122.59 | ops/s | 1.8x slower |
| openTelemetryClassic | 663.01 | ± 17.98 | ops/s | 8.1x slower |
| openTelemetryExponential | 562.58 | ± 52.14 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.59K | ± 8.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.18K | ± 6.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.89K | ± 5.83K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 494.65K | ± 7.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50039.968    ± 838.463  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.640     ± 38.465  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1230.429      ± 4.485  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1236.392     ± 52.839  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50480.390   ± 1642.092  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66074.182    ± 424.933  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56287.535   ± 1368.535  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6338.156    ± 193.203  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6623.146     ± 86.605  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6416.342    ± 149.372  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.009     ± 17.981  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.583     ± 52.140  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5388.992    ± 170.376  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.663    ± 122.591  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4428.453     ± 66.794  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     494645.142   ± 7502.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506888.649   ± 5827.663  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521175.021   ± 6781.485  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526588.256   ± 8207.371  ops/s
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
