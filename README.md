# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-06T06:34:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.56K | ± 55.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.27K | ± 229.15 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.94K | ± 1.18K | ops/s | 1.1x slower |
| prometheusAdd | 27.77K | ± 1.28K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.92K | ± 90.38 | ops/s | 4.6x slower |
| simpleclientInc | 6.75K | ± 48.53 | ops/s | 4.7x slower |
| simpleclientAdd | 6.49K | ± 50.67 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.48K | ± 47.91 | ops/s | 21x slower |
| openTelemetryInc | 1.41K | ± 79.07 | ops/s | 22x slower |
| openTelemetryAdd | 1.36K | ± 117.61 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 24.18 | ops/s | **fastest** |
| prometheusClassic | 3.18K | ± 229.56 | ops/s | 1.4x slower |
| prometheusNative | 2.19K | ± 151.39 | ops/s | 2.1x slower |
| openTelemetryClassic | 483.86 | ± 35.11 | ops/s | 9.3x slower |
| openTelemetryExponential | 392.54 | ± 7.03 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 338.95K | ± 2.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 336.75K | ± 1.45K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 311.01K | ± 2.66K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 307.69K | ± 2.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28940.962   ± 1178.970  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1356.700    ± 117.612  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1413.338     ± 79.073  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1478.490     ± 47.909  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27769.015   ± 1283.090  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31557.984     ± 55.482  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31270.281    ± 229.151  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6490.758     ± 50.672  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6751.385     ± 48.532  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6921.115     ± 90.384  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        483.856     ± 35.111  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        392.543      ± 7.030  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3178.521    ± 229.559  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2190.972    ± 151.391  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.629     ± 24.184  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     307685.298   ± 2226.547  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     311013.611   ± 2659.115  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     336751.680   ± 1450.337  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     338948.165   ± 2550.824  ops/s
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
