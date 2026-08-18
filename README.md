# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-18T04:11:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 65.71K | ± 694.21 | ops/s | **fastest** |
| prometheusInc | 65.33K | ± 2.51K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 62.37K | ± 2.95K | ops/s | 1.1x slower |
| prometheusAdd | 58.71K | ± 2.04K | ops/s | 1.1x slower |
| simpleclientInc | 10.56K | ± 147.17 | ops/s | 6.2x slower |
| simpleclientNoLabelsInc | 10.46K | ± 150.18 | ops/s | 6.3x slower |
| simpleclientAdd | 10.36K | ± 342.22 | ops/s | 6.3x slower |
| openTelemetryInc | 1.97K | ± 255.19 | ops/s | 33x slower |
| openTelemetryIncNoLabels | 1.93K | ± 231.33 | ops/s | 34x slower |
| openTelemetryAdd | 1.88K | ± 91.78 | ops/s | 35x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.48K | ± 69.07 | ops/s | **fastest** |
| simpleclient | 6.76K | ± 92.32 | ops/s | 1.1x slower |
| prometheusNative | 5.38K | ± 62.91 | ops/s | 1.4x slower |
| openTelemetryClassic | 843.44 | ± 32.29 | ops/s | 8.9x slower |
| openTelemetryExponential | 713.21 | ± 15.41 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 798.41K | ± 39.42K | ops/s | **fastest** |
| openMetricsWriteToNull | 716.61K | ± 46.10K | ops/s | 1.1x slower |
| prometheusWriteToByteArray | 716.52K | ± 15.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 699.93K | ± 17.36K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      62369.850   ± 2951.026  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1881.970     ± 91.778  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1968.372    ± 255.186  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1930.262    ± 231.328  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58712.687   ± 2036.281  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65330.685   ± 2514.598  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65708.416    ± 694.209  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10355.370    ± 342.218  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10555.561    ± 147.175  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10461.337    ± 150.177  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        843.439     ± 32.294  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        713.211     ± 15.408  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7484.970     ± 69.070  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5379.361     ± 62.907  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6756.394     ± 92.321  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     699934.845  ± 17364.989  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     716607.417  ± 46101.117  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     716515.681  ± 15233.251  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     798408.203  ± 39418.141  ops/s
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
