# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-24T07:19:09Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 52.61K | ± 85.59 | ops/s | **fastest** |
| prometheusInc | 51.94K | ± 12.57K | ops/s | 1.0x slower |
| prometheusAdd | 48.33K | ± 1.03K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 43.99K | ± 134.56 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 6.26K | ± 34.57 | ops/s | 8.4x slower |
| simpleclientInc | 6.24K | ± 36.49 | ops/s | 8.4x slower |
| simpleclientAdd | 5.99K | ± 292.06 | ops/s | 8.8x slower |
| openTelemetryIncNoLabels | 1.43K | ± 66.10 | ops/s | 37x slower |
| openTelemetryAdd | 1.32K | ± 77.21 | ops/s | 40x slower |
| openTelemetryInc | 1.31K | ± 89.26 | ops/s | 40x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.99K | ± 781.87 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 71.85 | ops/s | 1.1x slower |
| prometheusNative | 3.19K | ± 40.02 | ops/s | 1.6x slower |
| openTelemetryClassic | 601.96 | ± 17.05 | ops/s | 8.3x slower |
| openTelemetryExponential | 513.91 | ± 6.82 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 645.64K | ± 4.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 637.71K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 611.53K | ± 3.30K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 599.69K | ± 3.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43985.422    ± 134.562  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1320.329     ± 77.215  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1305.336     ± 89.257  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1432.186     ± 66.100  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48331.142   ± 1025.398  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      51939.103  ± 12570.941  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52608.821     ± 85.585  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5993.858    ± 292.059  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6236.509     ± 36.493  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6257.183     ± 34.572  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        601.958     ± 17.046  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        513.907      ± 6.823  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4990.585    ± 781.873  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3187.733     ± 40.021  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4391.245     ± 71.852  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     599686.666   ± 3096.586  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     611527.009   ± 3296.036  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     637711.117   ± 3100.960  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     645644.120   ± 4368.550  ops/s
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
