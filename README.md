# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-27T13:41:06Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.57K | ± 1.74K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 109.90 | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 250.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.40K | ± 1.95K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.60K | ± 18.23 | ops/s | 9.9x slower |
| simpleclientInc | 6.50K | ± 217.33 | ops/s | 10x slower |
| simpleclientAdd | 6.04K | ± 356.69 | ops/s | 11x slower |
| openTelemetryAdd | 1.39K | ± 257.54 | ops/s | 47x slower |
| openTelemetryInc | 1.37K | ± 197.45 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.27K | ± 147.69 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 182.23 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 29.20 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 158.50 | ops/s | 1.8x slower |
| openTelemetryClassic | 655.49 | ± 5.43 | ops/s | 8.4x slower |
| openTelemetryExponential | 536.20 | ± 12.04 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 521.35K | ± 4.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.01K | ± 9.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.15K | ± 6.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.71K | ± 9.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49395.218   ± 1950.913  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1392.628    ± 257.535  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1370.370    ± 197.454  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1274.874    ± 147.689  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51116.211    ± 250.139  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65573.956   ± 1742.777  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57058.107    ± 109.901  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6036.472    ± 356.690  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6504.164    ± 217.327  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6602.319     ± 18.229  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        655.493      ± 5.426  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.198     ± 12.038  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5499.042    ± 182.230  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3001.657    ± 158.499  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.422     ± 29.198  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495713.923   ± 9283.383  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507146.518   ± 6346.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517007.990   ± 9462.974  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     521349.730   ± 4667.127  ops/s
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
