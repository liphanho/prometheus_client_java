# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-26T07:24:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 30.80K | ± 838.33 | ops/s | **fastest** |
| prometheusInc | 30.73K | ± 1.24K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.54K | ± 1.12K | ops/s | 1.0x slower |
| prometheusAdd | 28.43K | ± 16.45 | ops/s | 1.1x slower |
| simpleclientInc | 6.97K | ± 136.88 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.87K | ± 89.66 | ops/s | 4.5x slower |
| simpleclientAdd | 6.66K | ± 118.84 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.44K | ± 54.28 | ops/s | 21x slower |
| openTelemetryInc | 1.40K | ± 25.07 | ops/s | 22x slower |
| openTelemetryAdd | 1.37K | ± 60.69 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 115.91 | ops/s | **fastest** |
| prometheusClassic | 3.07K | ± 188.80 | ops/s | 1.5x slower |
| prometheusNative | 2.31K | ± 128.57 | ops/s | 2.0x slower |
| openTelemetryClassic | 529.95 | ± 17.95 | ops/s | 8.6x slower |
| openTelemetryExponential | 409.06 | ± 9.30 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.60K | ± 3.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 324.61K | ± 2.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 304.74K | ± 6.09K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 302.66K | ± 2.88K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30799.888    ± 838.331  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1372.085     ± 60.692  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1401.532     ± 25.072  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1437.255     ± 54.276  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28426.579     ± 16.445  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30727.234   ± 1236.421  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30544.436   ± 1119.265  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6657.579    ± 118.835  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6966.850    ± 136.876  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6874.971     ± 89.658  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        529.951     ± 17.952  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        409.059      ± 9.300  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3067.564    ± 188.802  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2310.424    ± 128.567  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4533.167    ± 115.915  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     302663.095   ± 2882.448  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     304736.970   ± 6091.263  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     324613.015   ± 2680.325  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327595.190   ± 3249.828  ops/s
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
