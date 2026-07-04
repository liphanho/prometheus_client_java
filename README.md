# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T07:03:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.30K | ± 830.74 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.03K | ± 356.86 | ops/s | 1.2x slower |
| prometheusAdd | 45.59K | ± 3.63K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.03K | ± 6.07K | ops/s | 1.5x slower |
| simpleclientInc | 6.25K | ± 158.80 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.21K | ± 136.56 | ops/s | 9.7x slower |
| simpleclientAdd | 5.94K | ± 246.16 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 90.03 | ops/s | 44x slower |
| openTelemetryInc | 1.31K | ± 54.25 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.29K | ± 89.73 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.40K | ± 58.70 | ops/s | **fastest** |
| prometheusClassic | 4.18K | ± 849.94 | ops/s | 1.1x slower |
| prometheusNative | 3.10K | ± 136.87 | ops/s | 1.4x slower |
| openTelemetryClassic | 615.28 | ± 20.71 | ops/s | 7.1x slower |
| openTelemetryExponential | 483.64 | ± 17.49 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 641.46K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 626.02K | ± 13.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 596.57K | ± 4.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 593.92K | ± 7.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41025.696   ± 6072.726  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1368.249     ± 90.027  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1306.375     ± 54.253  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1285.953     ± 89.727  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      45594.900   ± 3629.191  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60299.880    ± 830.741  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52028.602    ± 356.860  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5937.810    ± 246.162  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6247.589    ± 158.805  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6211.762    ± 136.561  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        615.283     ± 20.709  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        483.638     ± 17.495  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4180.127    ± 849.938  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3098.401    ± 136.867  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.413     ± 58.695  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     593920.381   ± 7288.436  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     596574.885   ± 4249.738  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     626023.702  ± 13491.099  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     641461.589   ± 3628.779  ops/s
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
