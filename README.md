# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-25T12:12:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6975P-C, 4 cores, 15 GB RAM
- **OS:** Linux 7.0.0-1014-aws

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 33.72K | ± 60.71 | ops/s | **fastest** |
| prometheusInc | 33.44K | ± 704.97 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 33.13K | ± 1.36K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 32.08K | ± 294.45 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.52K | ± 38.39 | ops/s | 4.5x slower |
| simpleclientInc | 7.52K | ± 26.39 | ops/s | 4.5x slower |
| simpleclientAdd | 7.49K | ± 129.91 | ops/s | 4.5x slower |
| openTelemetryIncNoLabels | 994.37 | ± 56.69 | ops/s | 34x slower |
| openTelemetryAdd | 893.74 | ± 49.09 | ops/s | 38x slower |
| openTelemetryInc | 870.45 | ± 98.36 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.30K | ± 70.15 | ops/s | **fastest** |
| prometheusClassic | 2.90K | ± 232.79 | ops/s | 1.8x slower |
| prometheusNative | 1.88K | ± 158.73 | ops/s | 2.8x slower |
| openTelemetryClassic | 356.34 | ± 19.49 | ops/s | 15x slower |
| openTelemetryExponential | 279.96 | ± 18.06 | ops/s | 19x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 446.13K | ± 7.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 440.73K | ± 7.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 416.63K | ± 9.54K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 411.04K | ± 3.36K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      33133.165   ± 1358.600  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        893.743     ± 49.090  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        870.448     ± 98.360  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        994.367     ± 56.688  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      33723.409     ± 60.714  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      33439.188    ± 704.972  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      32081.744    ± 294.449  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7491.827    ± 129.907  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7516.697     ± 26.392  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7517.708     ± 38.385  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        356.336     ± 19.492  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        279.959     ± 18.059  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2898.643    ± 232.792  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1876.916    ± 158.725  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5300.201     ± 70.148  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     411035.880   ± 3361.648  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     416626.571   ± 9543.517  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     440729.768   ± 7807.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     446134.393   ± 7217.254  ops/s
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
