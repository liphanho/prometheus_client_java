# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-18T11:04:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 73.42K | ± 7.27K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.95K | ± 826.13 | ops/s | 1.1x slower |
| prometheusAdd | 62.53K | ± 1.47K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.03K | ± 1.47K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 7.93K | ± 67.20 | ops/s | 9.3x slower |
| simpleclientInc | 7.88K | ± 80.48 | ops/s | 9.3x slower |
| simpleclientAdd | 7.66K | ± 316.74 | ops/s | 9.6x slower |
| openTelemetryAdd | 1.88K | ± 225.67 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.83K | ± 153.10 | ops/s | 40x slower |
| openTelemetryInc | 1.74K | ± 29.46 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.43K | ± 997.95 | ops/s | **fastest** |
| simpleclient | 5.72K | ± 84.42 | ops/s | 1.1x slower |
| prometheusNative | 4.03K | ± 133.81 | ops/s | 1.6x slower |
| openTelemetryClassic | 828.29 | ± 11.91 | ops/s | 7.8x slower |
| openTelemetryExponential | 659.24 | ± 12.97 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 745.56K | ± 16.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 728.29K | ± 6.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 695.18K | ± 4.57K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 662.67K | ± 9.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55034.317   ± 1466.843  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1876.523    ± 225.669  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1744.655     ± 29.459  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1832.361    ± 153.097  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62530.008   ± 1474.056  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      73419.485   ± 7270.756  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65945.748    ± 826.128  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7661.053    ± 316.736  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7883.977     ± 80.477  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7930.621     ± 67.198  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        828.287     ± 11.905  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        659.241     ± 12.965  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6425.386    ± 997.954  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4029.092    ± 133.810  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5721.730     ± 84.424  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     662671.732   ± 9457.646  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     695181.679   ± 4569.856  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     728289.038   ± 6724.284  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     745562.647  ± 16690.601  ops/s
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
