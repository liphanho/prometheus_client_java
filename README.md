# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-19T08:23:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 51.45K | ± 12.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.39K | ± 418.55 | ops/s | 1.0x slower |
| prometheusAdd | 48.51K | ± 1.12K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 44.44K | ± 521.98 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 6.23K | ± 9.61 | ops/s | 8.3x slower |
| simpleclientAdd | 6.16K | ± 33.76 | ops/s | 8.4x slower |
| simpleclientInc | 6.07K | ± 105.12 | ops/s | 8.5x slower |
| openTelemetryAdd | 1.41K | ± 60.17 | ops/s | 36x slower |
| openTelemetryInc | 1.39K | ± 112.00 | ops/s | 37x slower |
| openTelemetryIncNoLabels | 1.38K | ± 106.21 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.89K | ± 918.11 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 176.30 | ops/s | 1.1x slower |
| prometheusNative | 3.08K | ± 75.20 | ops/s | 1.6x slower |
| openTelemetryClassic | 641.50 | ± 5.77 | ops/s | 7.6x slower |
| openTelemetryExponential | 509.52 | ± 26.57 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 615.82K | ± 4.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 606.79K | ± 2.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 585.89K | ± 3.20K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 576.64K | ± 3.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44437.461    ± 521.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1411.475     ± 60.166  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1385.299    ± 112.001  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1377.463    ± 106.207  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48514.376   ± 1121.505  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      51451.783  ± 12101.672  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51393.739    ± 418.553  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6158.313     ± 33.760  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6067.035    ± 105.118  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6228.340      ± 9.605  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        641.498      ± 5.773  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        509.524     ± 26.573  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4886.730    ± 918.114  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3076.400     ± 75.205  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4513.558    ± 176.300  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     576643.808   ± 3081.167  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     585885.242   ± 3200.552  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     606785.138   ± 2671.299  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     615817.553   ± 4638.861  ops/s
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
