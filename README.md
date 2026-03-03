# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-03T05:32:49Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.58K | ± 38.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.02K | ± 143.91 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.26K | ± 57.09 | ops/s | 1.1x slower |
| prometheusAdd | 28.63K | ± 105.47 | ops/s | 1.1x slower |
| simpleclientInc | 6.91K | ± 50.24 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.85K | ± 263.87 | ops/s | 4.6x slower |
| simpleclientAdd | 6.77K | ± 52.32 | ops/s | 4.7x slower |
| openTelemetryInc | 1.44K | ± 81.27 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.43K | ± 127.82 | ops/s | 22x slower |
| openTelemetryAdd | 1.39K | ± 20.48 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 67.34 | ops/s | **fastest** |
| prometheusClassic | 2.96K | ± 207.14 | ops/s | 1.5x slower |
| prometheusNative | 2.18K | ± 261.06 | ops/s | 2.1x slower |
| openTelemetryClassic | 525.61 | ± 31.45 | ops/s | 8.6x slower |
| openTelemetryExponential | 428.97 | ± 57.07 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 342.21K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 337.37K | ± 3.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.12K | ± 1.90K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 311.38K | ± 750.50 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29258.773     ± 57.093  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1391.546     ± 20.483  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1440.156     ± 81.268  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1426.507    ± 127.820  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28631.214    ± 105.473  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31575.842     ± 38.048  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31020.447    ± 143.913  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6770.799     ± 52.320  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6908.669     ± 50.244  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6853.639    ± 263.872  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        525.612     ± 31.452  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        428.967     ± 57.071  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2958.255    ± 207.140  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2176.717    ± 261.056  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4514.201     ± 67.335  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     311379.419    ± 750.499  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     312115.301   ± 1899.672  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     337370.207   ± 3277.012  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     342209.738   ± 3596.978  ops/s
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
