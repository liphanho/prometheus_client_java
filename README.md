# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-23T08:43:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.57K | ± 39.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.42K | ± 142.69 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.28K | ± 192.69 | ops/s | 1.1x slower |
| prometheusAdd | 27.94K | ± 792.30 | ops/s | 1.1x slower |
| simpleclientInc | 7.02K | ± 59.40 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.79K | ± 113.28 | ops/s | 4.6x slower |
| simpleclientAdd | 6.54K | ± 234.02 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.31K | ± 50.07 | ops/s | 24x slower |
| openTelemetryAdd | 1.28K | ± 42.91 | ops/s | 25x slower |
| openTelemetryInc | 1.27K | ± 85.47 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 79.64 | ops/s | **fastest** |
| prometheusClassic | 2.96K | ± 140.28 | ops/s | 1.5x slower |
| prometheusNative | 2.11K | ± 229.61 | ops/s | 2.1x slower |
| openTelemetryClassic | 510.01 | ± 18.10 | ops/s | 8.7x slower |
| openTelemetryExponential | 408.91 | ± 11.55 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 340.53K | ± 2.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 339.42K | ± 1.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 313.69K | ± 2.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 309.89K | ± 1.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29275.626    ± 192.691  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1277.515     ± 42.915  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1269.145     ± 85.465  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1313.599     ± 50.065  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27937.487    ± 792.299  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31572.773     ± 39.326  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31418.054    ± 142.693  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6538.561    ± 234.024  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7019.430     ± 59.405  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6793.542    ± 113.280  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        510.006     ± 18.102  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        408.906     ± 11.555  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2962.554    ± 140.279  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2111.142    ± 229.607  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.801     ± 79.642  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     309885.031   ± 1227.353  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     313685.436   ± 2231.221  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     339418.029   ± 1823.093  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     340525.280   ± 2333.804  ops/s
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
