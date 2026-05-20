# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-20T07:25:39Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.83K | ± 96.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.34K | ± 1.43K | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 130.13 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.93K | ± 1.39K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.52K | ± 143.17 | ops/s | 10x slower |
| simpleclientInc | 6.46K | ± 199.77 | ops/s | 10x slower |
| simpleclientAdd | 6.36K | ± 181.02 | ops/s | 10x slower |
| openTelemetryAdd | 1.62K | ± 270.18 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.37K | ± 130.89 | ops/s | 48x slower |
| openTelemetryInc | 1.30K | ± 27.85 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 285.75 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 116.90 | ops/s | 1.3x slower |
| prometheusNative | 3.15K | ± 78.49 | ops/s | 1.7x slower |
| openTelemetryClassic | 689.53 | ± 14.42 | ops/s | 7.9x slower |
| openTelemetryExponential | 552.44 | ± 28.26 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 531.06K | ± 4.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.09K | ± 2.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.70K | ± 1.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 504.42K | ± 3.14K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48926.853   ± 1388.652  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1623.168    ± 270.176  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1300.517     ± 27.845  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1373.190    ± 130.888  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51486.124    ± 130.130  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65825.606     ± 96.595  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55335.789   ± 1426.017  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6364.124    ± 181.024  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6457.862    ± 199.765  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6524.890    ± 143.172  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.529     ± 14.420  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.437     ± 28.257  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5471.076    ± 285.747  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.453     ± 78.495  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4324.818    ± 116.898  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     504417.121   ± 3142.336  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521704.352   ± 1819.031  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527087.023   ± 2216.688  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531058.842   ± 4153.178  ops/s
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
