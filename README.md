# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-05T05:54:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.12K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 50.93K | ± 540.67 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.64K | ± 7.68K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.60K | ± 59.38 | ops/s | 9.9x slower |
| simpleclientInc | 6.52K | ± 106.81 | ops/s | 10.0x slower |
| simpleclientAdd | 6.36K | ± 207.97 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.37K | ± 153.96 | ops/s | 47x slower |
| openTelemetryAdd | 1.24K | ± 6.05 | ops/s | 53x slower |
| openTelemetryInc | 1.23K | ± 30.91 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 45.55 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 44.98 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 130.68 | ops/s | 1.7x slower |
| openTelemetryClassic | 699.31 | ± 19.77 | ops/s | 7.5x slower |
| openTelemetryExponential | 581.07 | ± 17.24 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.61K | ± 9.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.99K | ± 5.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.18K | ± 9.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 508.00K | ± 7.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43642.544   ± 7684.645  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1238.841      ± 6.045  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1233.847     ± 30.905  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1374.141    ± 153.962  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50929.363    ± 540.666  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65118.615   ± 1383.602  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56375.138   ± 1073.335  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6362.397    ± 207.975  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6520.383    ± 106.814  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6598.868     ± 59.380  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.311     ± 19.765  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        581.068     ± 17.235  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5239.284     ± 45.547  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3073.393    ± 130.677  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4471.758     ± 44.982  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508000.491   ± 7750.378  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509181.158   ± 9753.401  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529993.710   ± 5935.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551605.821   ± 9419.166  ops/s
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
