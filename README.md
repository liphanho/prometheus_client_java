# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-28T05:12:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.77K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.90K | ± 416.50 | ops/s | 1.1x slower |
| prometheusAdd | 51.15K | ± 409.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.95K | ± 8.41K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 44.58 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.48K | ± 170.61 | ops/s | 10.0x slower |
| simpleclientAdd | 6.12K | ± 348.82 | ops/s | 11x slower |
| openTelemetryAdd | 1.69K | ± 71.55 | ops/s | 38x slower |
| openTelemetryInc | 1.43K | ± 179.90 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.34K | ± 137.63 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.58K | ± 216.80 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 18.73 | ops/s | 1.2x slower |
| prometheusNative | 3.21K | ± 48.79 | ops/s | 1.7x slower |
| openTelemetryClassic | 672.24 | ± 6.04 | ops/s | 8.3x slower |
| openTelemetryExponential | 529.23 | ± 34.38 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 543.55K | ± 2.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.20K | ± 5.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.27K | ± 7.02K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 511.76K | ± 4.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44945.382   ± 8410.035  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1694.479     ± 71.548  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.424    ± 179.902  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1336.563    ± 137.629  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51145.653    ± 409.400  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64770.852   ± 1014.201  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56903.978    ± 416.502  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6117.189    ± 348.822  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6770.628     ± 44.576  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6484.623    ± 170.610  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.242      ± 6.041  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.230     ± 34.379  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5583.589    ± 216.801  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3208.306     ± 48.791  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.830     ± 18.731  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511763.122   ± 4655.395  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512269.557   ± 7021.547  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540201.453   ± 5737.606  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     543551.406   ± 2151.089  ops/s
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
