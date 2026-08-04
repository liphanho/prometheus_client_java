# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-04T06:32:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.89K | ± 728.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.35K | ± 524.96 | ops/s | 1.1x slower |
| prometheusAdd | 48.57K | ± 87.38 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.23K | ± 191.82 | ops/s | 1.3x slower |
| simpleclientInc | 6.27K | ± 62.18 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.00K | ± 225.02 | ops/s | 9.8x slower |
| simpleclientAdd | 5.87K | ± 275.38 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 143.82 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.36K | ± 42.19 | ops/s | 43x slower |
| openTelemetryAdd | 1.35K | ± 25.45 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 458.65 | ops/s | **fastest** |
| simpleclient | 4.30K | ± 59.02 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 115.62 | ops/s | 1.7x slower |
| openTelemetryClassic | 603.02 | ± 20.77 | ops/s | 8.8x slower |
| openTelemetryExponential | 530.87 | ± 8.95 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 645.59K | ± 5.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 636.41K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 610.79K | ± 5.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.80K | ± 3.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44232.183    ± 191.817  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1345.255     ± 25.446  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1424.471    ± 143.820  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1360.092     ± 42.191  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48572.431     ± 87.384  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58885.953    ± 728.333  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52350.225    ± 524.964  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5873.151    ± 275.383  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6268.197     ± 62.178  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5999.076    ± 225.025  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        603.024     ± 20.775  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.868      ± 8.951  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5300.642    ± 458.650  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3092.667    ± 115.617  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4301.052     ± 59.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597804.087   ± 3267.078  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     610788.455   ± 5777.773  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     636413.895   ± 5816.872  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     645586.255   ± 5667.168  ops/s
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
