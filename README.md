# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-01T05:40:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 55.96K | ± 652.51 | ops/s | **fastest** |
| prometheusInc | 53.68K | ± 15.72K | ops/s | 1.0x slower |
| prometheusAdd | 51.33K | ± 423.08 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.45K | ± 1.49K | ops/s | 1.1x slower |
| simpleclientInc | 6.78K | ± 15.43 | ops/s | 8.3x slower |
| simpleclientNoLabelsInc | 6.69K | ± 22.62 | ops/s | 8.4x slower |
| simpleclientAdd | 6.29K | ± 210.60 | ops/s | 8.9x slower |
| openTelemetryAdd | 1.29K | ± 41.73 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.28K | ± 146.79 | ops/s | 44x slower |
| openTelemetryInc | 1.20K | ± 54.73 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.17K | ± 422.14 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 24.36 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 183.87 | ops/s | 1.8x slower |
| openTelemetryClassic | 661.46 | ± 41.59 | ops/s | 7.8x slower |
| openTelemetryExponential | 552.37 | ± 39.42 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 534.14K | ± 2.91K | ops/s | **fastest** |
| prometheusWriteToNull | 532.62K | ± 16.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.36K | ± 11.87K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.17K | ± 12.25K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49445.140   ± 1493.640  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1286.748     ± 41.732  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1198.703     ± 54.730  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1277.121    ± 146.792  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51327.162    ± 423.078  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      53677.567  ± 15718.697  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55956.711    ± 652.511  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6293.189    ± 210.603  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6778.085     ± 15.435  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6686.243     ± 22.624  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.463     ± 41.593  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.373     ± 39.417  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5174.115    ± 422.144  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2943.683    ± 183.874  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4509.126     ± 24.362  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510169.717  ± 12251.549  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519364.036  ± 11870.653  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534140.897   ± 2908.909  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532617.908  ± 16789.614  ops/s
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
