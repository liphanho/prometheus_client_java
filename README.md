# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-15T05:49:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.34K | ± 3.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 555.16 | ops/s | 1.1x slower |
| prometheusAdd | 51.13K | ± 717.35 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.82K | ± 416.28 | ops/s | 1.3x slower |
| simpleclientInc | 6.68K | ± 123.24 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.62K | ± 138.66 | ops/s | 9.6x slower |
| simpleclientAdd | 6.14K | ± 62.43 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 189.64 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.30K | ± 46.14 | ops/s | 49x slower |
| openTelemetryInc | 1.25K | ± 60.17 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 109.29 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 26.57 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 101.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 679.21 | ± 2.19 | ops/s | 7.9x slower |
| openTelemetryExponential | 583.71 | ± 21.64 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.05K | ± 7.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.53K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.37K | ± 8.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.70K | ± 9.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48819.928    ± 416.275  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1429.896    ± 189.643  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1246.166     ± 60.175  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1300.922     ± 46.144  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51133.050    ± 717.355  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63340.833   ± 3857.429  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56846.069    ± 555.161  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6144.007     ± 62.434  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6681.682    ± 123.245  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6618.892    ± 138.662  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.211      ± 2.192  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.714     ± 21.639  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5364.808    ± 109.294  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3050.996    ± 101.704  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4534.791     ± 26.574  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499699.985   ± 9540.433  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505367.823   ± 8667.565  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512533.183   ± 4109.852  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527050.041   ± 7907.248  ops/s
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
