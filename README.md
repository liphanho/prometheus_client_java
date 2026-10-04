# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-04T09:06:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.08K | ± 567.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.12K | ± 1.01K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 62.77K | ± 550.34 | ops/s | 1.1x slower |
| prometheusAdd | 59.56K | ± 1.81K | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 10.98K | ± 141.27 | ops/s | 6.3x slower |
| simpleclientAdd | 10.48K | ± 371.15 | ops/s | 6.6x slower |
| simpleclientInc | 10.42K | ± 198.90 | ops/s | 6.6x slower |
| openTelemetryInc | 2.04K | ± 213.90 | ops/s | 34x slower |
| openTelemetryIncNoLabels | 1.84K | ± 16.91 | ops/s | 38x slower |
| openTelemetryAdd | 1.77K | ± 32.95 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.43K | ± 152.26 | ops/s | **fastest** |
| simpleclient | 6.87K | ± 205.09 | ops/s | 1.1x slower |
| prometheusNative | 5.27K | ± 437.74 | ops/s | 1.4x slower |
| openTelemetryClassic | 894.38 | ± 63.40 | ops/s | 8.3x slower |
| openTelemetryExponential | 680.46 | ± 16.41 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 771.78K | ± 25.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 768.58K | ± 32.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 731.39K | ± 38.44K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 682.86K | ± 19.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      62770.189    ± 550.335  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1770.553     ± 32.951  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2044.863    ± 213.903  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1841.856     ± 16.911  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59560.092   ± 1811.928  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69081.550    ± 567.664  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66117.958   ± 1009.676  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10481.409    ± 371.147  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10418.276    ± 198.902  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10977.523    ± 141.269  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        894.379     ± 63.400  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        680.459     ± 16.410  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7434.642    ± 152.258  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5270.052    ± 437.739  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6872.204    ± 205.089  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     731391.002  ± 38443.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     682856.781  ± 19787.307  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     768580.573  ± 32761.451  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     771783.463  ± 25770.503  ops/s
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
