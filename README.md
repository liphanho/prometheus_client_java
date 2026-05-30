# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-30T07:05:37Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.45K | ± 548.51 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.19K | ± 2.77K | ops/s | 1.2x slower |
| prometheusAdd | 50.96K | ± 747.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.68K | ± 744.88 | ops/s | 1.4x slower |
| simpleclientInc | 6.51K | ± 187.68 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 191.48 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 223.73 | ops/s | 11x slower |
| openTelemetryInc | 1.33K | ± 163.17 | ops/s | 50x slower |
| openTelemetryAdd | 1.28K | ± 30.90 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.18K | ± 38.45 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.15K | ± 283.09 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 38.69 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 135.55 | ops/s | 1.8x slower |
| openTelemetryClassic | 767.87 | ± 9.84 | ops/s | 6.7x slower |
| openTelemetryExponential | 569.44 | ± 4.93 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 519.71K | ± 8.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 502.82K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 500.67K | ± 3.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.87K | ± 5.27K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47677.795    ± 744.880  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.341     ± 30.896  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.011    ± 163.171  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1184.517     ± 38.445  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50964.884    ± 747.379  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66451.765    ± 548.513  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55189.967   ± 2773.645  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6143.780    ± 223.730  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6511.977    ± 187.682  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6400.704    ± 191.477  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        767.870      ± 9.842  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.438      ± 4.931  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5154.380    ± 283.088  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2938.076    ± 135.553  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.070     ± 38.693  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499874.517   ± 5267.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     500672.070   ± 3625.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502823.914   ± 5064.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     519712.555   ± 8851.405  ops/s
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
