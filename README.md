# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-10T07:41:37Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.05K | ± 252.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.03K | ± 1.27K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.18K | ± 2.40K | ops/s | 1.4x slower |
| prometheusAdd | 42.83K | ± 13.52K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.60K | ± 7.30 | ops/s | 10x slower |
| simpleclientInc | 6.55K | ± 46.77 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 200.51 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 206.84 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.35K | ± 188.68 | ops/s | 49x slower |
| openTelemetryInc | 1.22K | ± 13.55 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 139.82 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 42.13 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 53.94 | ops/s | 1.7x slower |
| openTelemetryClassic | 696.18 | ± 44.21 | ops/s | 7.7x slower |
| openTelemetryExponential | 561.28 | ± 8.71 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 526.62K | ± 10.59K | ops/s | **fastest** |
| prometheusWriteToNull | 525.34K | ± 5.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 517.01K | ± 7.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 497.25K | ± 5.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48180.502   ± 2398.082  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1369.216    ± 206.841  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1223.876     ± 13.550  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1345.610    ± 188.680  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      42826.780  ± 13519.805  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66047.644    ± 252.661  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56032.954   ± 1267.840  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6152.361    ± 200.514  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6548.614     ± 46.768  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6599.274      ± 7.300  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.180     ± 44.205  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.278      ± 8.706  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5364.672    ± 139.819  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3131.801     ± 53.939  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.350     ± 42.130  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497249.417   ± 5222.546  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     517012.965   ± 7760.008  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526618.795  ± 10586.050  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     525344.580   ± 5807.010  ops/s
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
