# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T08:12:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.79K | ± 335.75 | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.78K | ± 68.25 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 65.46K | ± 3.56K | ops/s | 1.1x slower |
| prometheusAdd | 58.45K | ± 134.43 | ops/s | 1.2x slower |
| simpleclientInc | 11.21K | ± 115.85 | ops/s | 6.2x slower |
| simpleclientNoLabelsInc | 11.07K | ± 322.53 | ops/s | 6.3x slower |
| simpleclientAdd | 10.88K | ± 296.69 | ops/s | 6.4x slower |
| openTelemetryAdd | 2.18K | ± 232.34 | ops/s | 32x slower |
| openTelemetryIncNoLabels | 2.18K | ± 239.81 | ops/s | 32x slower |
| openTelemetryInc | 1.83K | ± 73.00 | ops/s | 38x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.47K | ± 258.48 | ops/s | **fastest** |
| simpleclient | 7.19K | ± 60.14 | ops/s | 1.0x slower |
| prometheusNative | 5.49K | ± 418.03 | ops/s | 1.4x slower |
| openTelemetryClassic | 898.12 | ± 23.30 | ops/s | 8.3x slower |
| openTelemetryExponential | 698.76 | ± 22.01 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 811.37K | ± 38.03K | ops/s | **fastest** |
| prometheusWriteToNull | 794.91K | ± 30.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 748.42K | ± 44.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 725.02K | ± 26.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      65462.912   ± 3559.095  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2178.910    ± 232.343  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1831.287     ± 72.995  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2176.194    ± 239.805  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58451.684    ± 134.427  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69785.756    ± 335.745  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67779.788     ± 68.253  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10883.281    ± 296.687  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11211.959    ± 115.851  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11071.948    ± 322.526  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        898.119     ± 23.305  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        698.757     ± 22.012  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7473.056    ± 258.478  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5487.875    ± 418.029  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7188.335     ± 60.136  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     725024.248  ± 26678.767  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     748418.775  ± 44217.969  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     811374.361  ± 38027.086  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     794908.544  ± 30541.360  ops/s
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
