# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-30T09:22:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.16K | ± 534.11 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.54K | ± 485.46 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 56.47K | ± 9.77K | ops/s | 1.2x slower |
| prometheusAdd | 54.79K | ± 411.24 | ops/s | 1.2x slower |
| simpleclientInc | 10.45K | ± 88.77 | ops/s | 6.3x slower |
| simpleclientNoLabelsInc | 10.39K | ± 164.48 | ops/s | 6.4x slower |
| simpleclientAdd | 10.22K | ± 80.91 | ops/s | 6.5x slower |
| openTelemetryAdd | 1.92K | ± 241.18 | ops/s | 34x slower |
| openTelemetryInc | 1.75K | ± 25.25 | ops/s | 38x slower |
| openTelemetryIncNoLabels | 1.71K | ± 27.29 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.27K | ± 154.88 | ops/s | **fastest** |
| simpleclient | 6.69K | ± 90.34 | ops/s | 1.1x slower |
| prometheusNative | 5.34K | ± 93.31 | ops/s | 1.4x slower |
| openTelemetryClassic | 803.68 | ± 10.96 | ops/s | 9.0x slower |
| openTelemetryExponential | 675.39 | ± 13.42 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 759.54K | ± 28.45K | ops/s | **fastest** |
| prometheusWriteToNull | 726.06K | ± 33.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 710.08K | ± 41.78K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 704.56K | ± 51.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56466.205   ± 9772.243  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1918.709    ± 241.183  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1748.794     ± 25.248  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1711.257     ± 27.293  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      54792.687    ± 411.238  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66162.410    ± 534.109  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65536.575    ± 485.458  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10215.877     ± 80.911  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10451.810     ± 88.775  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10388.037    ± 164.480  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        803.682     ± 10.955  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        675.395     ± 13.421  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7266.919    ± 154.882  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5339.266     ± 93.310  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6688.885     ± 90.343  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     710078.910  ± 41779.646  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     704563.301  ± 51480.572  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     759539.881  ± 28447.539  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     726059.917  ± 33812.626  ops/s
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
