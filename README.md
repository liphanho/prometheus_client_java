# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-29T06:43:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.28K | ± 374.15 | ops/s | **fastest** |
| prometheusAdd | 48.95K | ± 647.93 | ops/s | 1.2x slower |
| prometheusNoLabelsInc | 48.40K | ± 3.95K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.47K | ± 733.62 | ops/s | 1.3x slower |
| simpleclientInc | 6.21K | ± 234.51 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.18K | ± 178.39 | ops/s | 9.6x slower |
| simpleclientAdd | 6.10K | ± 54.94 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.35K | ± 97.64 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.29K | ± 53.97 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 6.26 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.40K | ± 80.44 | ops/s | **fastest** |
| prometheusClassic | 4.39K | ± 17.17 | ops/s | 1.0x slower |
| prometheusNative | 3.11K | ± 118.44 | ops/s | 1.4x slower |
| openTelemetryClassic | 578.09 | ± 11.95 | ops/s | 7.6x slower |
| openTelemetryExponential | 486.74 | ± 12.96 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 639.91K | ± 3.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 631.40K | ± 6.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 608.40K | ± 7.76K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 595.89K | ± 4.58K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44467.602    ± 733.617  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1351.117     ± 97.638  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1262.740      ± 6.261  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1291.864     ± 53.967  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48953.793    ± 647.933  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59275.397    ± 374.154  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      48395.237   ± 3951.614  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6099.038     ± 54.938  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6212.031    ± 234.505  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6184.503    ± 178.387  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        578.091     ± 11.949  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        486.744     ± 12.961  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4390.396     ± 17.170  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3109.218    ± 118.443  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.698     ± 80.438  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     595887.996   ± 4580.354  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     608398.132   ± 7761.975  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     631403.176   ± 6340.678  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     639911.198   ± 3924.048  ops/s
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
