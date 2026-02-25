# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-25T05:38:42Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.45K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.44K | ± 604.75 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 309.86 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.59K | ± 1.21K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 137.29 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.47K | ± 213.67 | ops/s | 10.0x slower |
| simpleclientAdd | 6.42K | ± 204.86 | ops/s | 10x slower |
| openTelemetryAdd | 1.58K | ± 270.58 | ops/s | 41x slower |
| openTelemetryInc | 1.36K | ± 41.26 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 61.24 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.91K | ± 16.92 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 36.06 | ops/s | 1.1x slower |
| prometheusNative | 2.92K | ± 103.56 | ops/s | 1.7x slower |
| openTelemetryClassic | 700.54 | ± 13.27 | ops/s | 7.0x slower |
| openTelemetryExponential | 526.74 | ± 26.89 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.78K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 532.80K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.98K | ± 5.59K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.11K | ± 6.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49594.413   ± 1213.181  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1581.212    ± 270.578  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1360.612     ± 41.264  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1240.496     ± 61.238  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51613.971    ± 309.857  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64449.281   ± 1196.625  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55440.736    ± 604.753  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6422.409    ± 204.860  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.677    ± 137.288  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6474.386    ± 213.668  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.543     ± 13.266  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.737     ± 26.887  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4906.253     ± 16.919  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2918.751    ± 103.557  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4518.763     ± 36.064  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505113.936   ± 6443.368  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515975.086   ± 5588.366  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     532795.078   ± 5008.933  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535780.135   ± 3598.987  ops/s
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
