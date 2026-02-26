# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-26T05:35:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.13K | ± 1.89K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.49K | ± 1.05K | ops/s | 1.2x slower |
| prometheusAdd | 51.07K | ± 541.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.20K | ± 1.66K | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 31.89 | ops/s | 9.8x slower |
| simpleclientAdd | 6.52K | ± 28.75 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 164.20 | ops/s | 10x slower |
| openTelemetryAdd | 1.59K | ± 60.11 | ops/s | 42x slower |
| openTelemetryInc | 1.38K | ± 112.38 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.20K | ± 11.26 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 75.13 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 10.62 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 134.37 | ops/s | 1.7x slower |
| openTelemetryClassic | 691.93 | ± 27.02 | ops/s | 7.6x slower |
| openTelemetryExponential | 534.29 | ± 32.40 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 533.12K | ± 10.39K | ops/s | **fastest** |
| prometheusWriteToNull | 531.01K | ± 4.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.39K | ± 5.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.92K | ± 10.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49204.709   ± 1661.205  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1586.981     ± 60.106  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1381.128    ± 112.385  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1198.489     ± 11.258  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51072.738    ± 541.250  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66126.654   ± 1892.072  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56492.172   ± 1054.076  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6519.904     ± 28.746  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6750.426     ± 31.893  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6470.513    ± 164.201  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.932     ± 27.025  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.286     ± 32.400  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5264.560     ± 75.126  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3072.767    ± 134.371  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4498.076     ± 10.616  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507923.107  ± 10353.865  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512386.753   ± 5606.138  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533116.425  ± 10393.677  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531013.809   ± 4701.456  ops/s
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
