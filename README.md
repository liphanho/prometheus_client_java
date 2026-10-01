# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T09:40:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.29K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.99K | ± 1.19K | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 186.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.05K | ± 1.86K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.63K | ± 11.17 | ops/s | 9.8x slower |
| simpleclientInc | 6.51K | ± 299.88 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 242.10 | ops/s | 11x slower |
| openTelemetryInc | 1.35K | ± 153.09 | ops/s | 48x slower |
| openTelemetryAdd | 1.28K | ± 1.30 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 55.63 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 340.76 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 75.01 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 142.30 | ops/s | 1.7x slower |
| openTelemetryClassic | 716.79 | ± 38.95 | ops/s | 7.3x slower |
| openTelemetryExponential | 583.73 | ± 30.70 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 534.86K | ± 7.77K | ops/s | **fastest** |
| prometheusWriteToNull | 534.56K | ± 5.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.30K | ± 7.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.39K | ± 5.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48045.721   ± 1860.096  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1277.853      ± 1.298  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1353.457    ± 153.088  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1195.816     ± 55.634  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51642.642    ± 186.391  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65288.746   ± 1225.010  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55993.263   ± 1185.778  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6116.721    ± 242.103  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6508.396    ± 299.878  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6630.695     ± 11.168  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        716.788     ± 38.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.732     ± 30.703  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5241.654    ± 340.764  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3120.631    ± 142.302  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.779     ± 75.008  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514390.947   ± 5845.219  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521301.854   ± 7207.651  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534858.521   ± 7768.626  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534556.665   ± 5625.953  ops/s
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
