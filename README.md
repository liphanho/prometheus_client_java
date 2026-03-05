# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-05T05:29:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.02K | ± 87.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.83K | ± 921.60 | ops/s | 1.2x slower |
| prometheusAdd | 51.34K | ± 535.92 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.97K | ± 7.46K | ops/s | 1.5x slower |
| simpleclientInc | 6.81K | ± 13.80 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.57K | ± 216.69 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 320.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 170.09 | ops/s | 44x slower |
| openTelemetryInc | 1.36K | ± 110.89 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 44.14 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 410.98 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 49.91 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 107.51 | ops/s | 1.7x slower |
| openTelemetryClassic | 677.52 | ± 26.58 | ops/s | 7.7x slower |
| openTelemetryExponential | 583.26 | ± 24.80 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 542.26K | ± 3.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.46K | ± 3.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.64K | ± 6.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 505.97K | ± 6.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44974.284   ± 7455.817  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1506.791    ± 170.087  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1358.752    ± 110.893  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.109     ± 44.142  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51335.935    ± 535.917  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66020.354     ± 87.677  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55832.959    ± 921.601  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6212.495    ± 320.217  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6806.688     ± 13.802  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6565.517    ± 216.690  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.524     ± 26.579  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.265     ± 24.801  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5249.627    ± 410.976  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3086.725    ± 107.515  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4531.774     ± 49.908  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505968.303   ± 6420.127  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514643.914   ± 6782.109  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529462.965   ± 3973.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542256.499   ± 3231.154  ops/s
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
