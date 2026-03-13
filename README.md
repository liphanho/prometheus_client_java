# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-13T05:29:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.55K | ± 1.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.30K | ± 931.82 | ops/s | 1.2x slower |
| prometheusAdd | 51.20K | ± 697.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.09K | ± 2.35K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 110.98 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.63K | ± 119.03 | ops/s | 9.9x slower |
| simpleclientAdd | 6.24K | ± 225.29 | ops/s | 11x slower |
| openTelemetryInc | 1.37K | ± 135.49 | ops/s | 48x slower |
| openTelemetryAdd | 1.37K | ± 253.51 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 249.84 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 208.41 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 57.06 | ops/s | 1.1x slower |
| prometheusNative | 3.19K | ± 130.95 | ops/s | 1.6x slower |
| openTelemetryClassic | 678.40 | ± 28.21 | ops/s | 7.6x slower |
| openTelemetryExponential | 537.45 | ± 14.56 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 544.18K | ± 5.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.39K | ± 6.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.72K | ± 5.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.82K | ± 13.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49092.827   ± 2354.567  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1372.050    ± 253.508  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1372.756    ± 135.491  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1327.579    ± 249.836  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51196.531    ± 697.727  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65549.407   ± 1400.662  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56297.236    ± 931.819  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6240.797    ± 225.286  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.319    ± 110.983  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6632.243    ± 119.034  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.401     ± 28.206  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.452     ± 14.555  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5164.093    ± 208.407  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3194.705    ± 130.948  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.265     ± 57.057  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521720.012   ± 5383.685  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516824.788  ± 13461.141  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531389.929   ± 6729.656  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     544184.137   ± 5447.202  ops/s
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
