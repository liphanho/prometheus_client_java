# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-20T08:30:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.46K | ± 1.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 510.45 | ops/s | 1.2x slower |
| prometheusAdd | 49.19K | ± 2.62K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.39K | ± 1.93K | ops/s | 1.4x slower |
| simpleclientInc | 6.71K | ± 13.41 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.19K | ± 21.86 | ops/s | 11x slower |
| simpleclientAdd | 6.17K | ± 228.02 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 245.76 | ops/s | 48x slower |
| openTelemetryInc | 1.25K | ± 20.92 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.18K | ± 58.72 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 68.81 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 63.35 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 34.32 | ops/s | 1.7x slower |
| openTelemetryClassic | 648.29 | ± 15.16 | ops/s | 8.2x slower |
| openTelemetryExponential | 585.10 | ± 37.43 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.84K | ± 2.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 535.00K | ± 5.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.14K | ± 3.27K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 509.74K | ± 4.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48387.812   ± 1930.370  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1371.673    ± 245.760  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1253.111     ± 20.918  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1183.328     ± 58.723  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49192.910   ± 2623.788  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65459.210   ± 1647.944  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56690.866    ± 510.454  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6171.621    ± 228.024  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6705.707     ± 13.412  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6191.144     ± 21.864  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        648.291     ± 15.163  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.095     ± 37.428  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5290.371     ± 68.807  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3124.093     ± 34.316  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4447.916     ± 63.352  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510138.447   ± 3270.162  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509736.070   ± 4239.435  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     535003.166   ± 5991.320  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538840.746   ± 2936.003  ops/s
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
