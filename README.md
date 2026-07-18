# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T06:05:49Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.41K | ± 2.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 432.27 | ops/s | 1.1x slower |
| prometheusAdd | 50.80K | ± 648.64 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.72K | ± 630.71 | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 7.31 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.48K | ± 209.76 | ops/s | 9.8x slower |
| simpleclientAdd | 6.29K | ± 241.78 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 110.44 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.34K | ± 202.14 | ops/s | 47x slower |
| openTelemetryAdd | 1.31K | ± 67.70 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 29.92 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 63.85 | ops/s | 1.1x slower |
| prometheusNative | 3.10K | ± 181.69 | ops/s | 1.6x slower |
| openTelemetryClassic | 673.17 | ± 13.97 | ops/s | 7.5x slower |
| openTelemetryExponential | 570.47 | ± 8.29 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.88K | ± 8.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.99K | ± 5.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.53K | ± 7.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.97K | ± 4.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47717.221    ± 630.712  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1310.133     ± 67.696  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1363.829    ± 110.439  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1338.002    ± 202.143  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50796.793    ± 648.637  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63413.115   ± 2541.288  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56663.544    ± 432.268  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6293.621    ± 241.777  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6711.779      ± 7.308  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.314    ± 209.762  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.172     ± 13.973  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.465      ± 8.288  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5025.003     ± 29.922  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3096.784    ± 181.689  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4437.150     ± 63.848  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471971.426   ± 4482.418  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473526.534   ± 7549.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486987.196   ± 5915.710  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496881.852   ± 8716.332  ops/s
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
