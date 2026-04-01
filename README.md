# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-01T06:04:25Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 370.97 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 447.06 | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 66.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.79K | ± 1.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 42.37 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.54K | ± 104.48 | ops/s | 10x slower |
| simpleclientAdd | 6.17K | ± 258.45 | ops/s | 11x slower |
| openTelemetryAdd | 1.36K | ± 184.35 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.36K | ± 217.14 | ops/s | 49x slower |
| openTelemetryInc | 1.34K | ± 217.40 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 60.80 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 71.15 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 165.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 709.36 | ± 53.81 | ops/s | 7.5x slower |
| openTelemetryExponential | 594.28 | ± 22.08 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 546.74K | ± 4.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.07K | ± 4.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.32K | ± 5.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 525.00K | ± 3.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48789.839   ± 1034.564  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1363.618    ± 184.346  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1336.760    ± 217.400  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.879    ± 217.139  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51641.980     ± 66.037  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66176.017    ± 370.966  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56998.817    ± 447.061  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6166.240    ± 258.448  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6681.848     ± 42.365  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6542.601    ± 104.480  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        709.358     ± 53.806  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.276     ± 22.080  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5352.949     ± 60.805  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3018.141    ± 165.701  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.933     ± 71.147  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524996.743   ± 3850.069  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536320.402   ± 5384.490  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542074.385   ± 4905.043  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     546736.807   ± 4896.172  ops/s
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
