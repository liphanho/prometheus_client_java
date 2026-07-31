# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-31T06:52:37Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 32.12K | ± 68.74 | ops/s | **fastest** |
| prometheusInc | 30.87K | ± 57.59 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.66K | ± 355.32 | ops/s | 1.0x slower |
| prometheusAdd | 29.91K | ± 106.86 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.72K | ± 85.80 | ops/s | 4.2x slower |
| simpleclientInc | 7.71K | ± 33.69 | ops/s | 4.2x slower |
| simpleclientAdd | 7.50K | ± 140.50 | ops/s | 4.3x slower |
| openTelemetryAdd | 1.18K | ± 67.50 | ops/s | 27x slower |
| openTelemetryInc | 1.16K | ± 84.10 | ops/s | 28x slower |
| openTelemetryIncNoLabels | 1.12K | ± 63.58 | ops/s | 29x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.06K | ± 86.99 | ops/s | **fastest** |
| prometheusClassic | 2.73K | ± 150.07 | ops/s | 1.9x slower |
| prometheusNative | 2.15K | ± 36.62 | ops/s | 2.3x slower |
| openTelemetryClassic | 413.63 | ± 23.20 | ops/s | 12x slower |
| openTelemetryExponential | 335.41 | ± 14.99 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 309.46K | ± 1.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 306.77K | ± 2.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 291.71K | ± 1.50K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 288.71K | ± 1.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      32120.765     ± 68.737  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1180.956     ± 67.503  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1160.204     ± 84.099  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1116.185     ± 63.576  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29913.607    ± 106.856  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30874.249     ± 57.590  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30658.289    ± 355.323  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7497.608    ± 140.503  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7707.313     ± 33.688  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7722.120     ± 85.802  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        413.628     ± 23.202  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        335.413     ± 14.992  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2732.308    ± 150.075  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2154.408     ± 36.617  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5058.756     ± 86.994  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     288709.571   ± 1109.408  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     291714.959   ± 1499.473  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     306767.911   ± 2024.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     309463.193   ± 1452.884  ops/s
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
