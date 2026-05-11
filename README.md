# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-11T07:16:05Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.52K | ± 386.19 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 363.02 | ops/s | 1.2x slower |
| prometheusAdd | 48.28K | ± 265.34 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.38K | ± 2.19K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.24K | ± 92.85 | ops/s | 9.5x slower |
| simpleclientInc | 6.12K | ± 152.47 | ops/s | 9.7x slower |
| simpleclientAdd | 5.80K | ± 352.89 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 124.33 | ops/s | 41x slower |
| openTelemetryAdd | 1.32K | ± 18.17 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.31K | ± 28.89 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.01K | ± 522.04 | ops/s | **fastest** |
| simpleclient | 4.59K | ± 87.79 | ops/s | 1.1x slower |
| prometheusNative | 3.20K | ± 44.27 | ops/s | 1.6x slower |
| openTelemetryClassic | 638.41 | ± 36.83 | ops/s | 7.8x slower |
| openTelemetryExponential | 544.23 | ± 35.40 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 637.91K | ± 8.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 617.80K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 602.36K | ± 5.52K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 589.46K | ± 8.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43384.033   ± 2188.454  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1322.016     ± 18.174  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1460.104    ± 124.334  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.988     ± 28.886  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48275.259    ± 265.343  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59515.863    ± 386.193  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51466.478    ± 363.019  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5800.483    ± 352.886  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6119.482    ± 152.466  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6241.277     ± 92.845  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        638.409     ± 36.828  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.234     ± 35.402  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5010.371    ± 522.038  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3196.195     ± 44.274  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4594.653     ± 87.786  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     589460.625   ± 8113.361  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     602356.976   ± 5524.483  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     617801.553   ± 5061.128  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     637911.162   ± 8058.231  ops/s
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
