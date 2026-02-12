# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-12T05:42:28Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.05K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 337.81 | ops/s | 1.2x slower |
| prometheusAdd | 50.95K | ± 577.87 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.76K | ± 251.38 | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 206.65 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.57K | ± 176.40 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 173.73 | ops/s | 10x slower |
| openTelemetryInc | 1.48K | ± 209.77 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.39K | ± 199.27 | ops/s | 48x slower |
| openTelemetryAdd | 1.29K | ± 42.71 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.37K | ± 290.28 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 35.24 | ops/s | 1.2x slower |
| prometheusNative | 3.14K | ± 39.81 | ops/s | 1.7x slower |
| openTelemetryClassic | 640.61 | ± 7.29 | ops/s | 8.4x slower |
| openTelemetryExponential | 530.78 | ± 11.02 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 547.43K | ± 7.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.09K | ± 3.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.04K | ± 4.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 516.09K | ± 12.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47756.935    ± 251.384  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1285.525     ± 42.712  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1477.346    ± 209.768  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1386.063    ± 199.267  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50948.691    ± 577.866  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66053.464   ± 1705.545  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57062.205    ± 337.808  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6351.633    ± 173.728  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6654.612    ± 206.651  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6568.053    ± 176.399  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        640.608      ± 7.293  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.782     ± 11.025  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5372.722    ± 290.282  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3140.016     ± 39.812  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4456.298     ± 35.240  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516091.448  ± 12848.794  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522038.111   ± 4889.982  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539085.376   ± 3466.517  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     547430.087   ± 7142.023  ops/s
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
