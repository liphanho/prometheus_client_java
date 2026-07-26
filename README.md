# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T06:49:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.40K | ± 334.75 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.73K | ± 1.14K | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 135.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.26K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 159.97 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.26K | ± 78.46 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 207.52 | ops/s | 11x slower |
| openTelemetryAdd | 1.57K | ± 279.71 | ops/s | 42x slower |
| openTelemetryInc | 1.41K | ± 138.93 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.36K | ± 205.98 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 30.33 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 28.53 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 115.19 | ops/s | 1.7x slower |
| openTelemetryClassic | 662.73 | ± 31.08 | ops/s | 8.0x slower |
| openTelemetryExponential | 544.99 | ± 17.07 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.12K | ± 6.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.76K | ± 3.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.14K | ± 3.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.67K | ± 5.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48258.001   ± 1632.268  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1569.167    ± 279.709  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.730    ± 138.934  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1364.818    ± 205.981  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51584.729    ± 135.605  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65395.812    ± 334.748  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55725.134   ± 1137.659  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6197.266    ± 207.516  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.657    ± 159.967  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6264.151     ± 78.461  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.731     ± 31.076  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.991     ± 17.066  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5298.854     ± 30.327  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3065.189    ± 115.189  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.836     ± 28.529  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486137.769   ± 3048.530  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483668.681   ± 5585.841  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499757.875   ± 3906.939  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509121.533   ± 6089.243  ops/s
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
