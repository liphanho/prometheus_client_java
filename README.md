# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T08:47:07Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.21K | ± 1.92K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 64.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.24K | ± 806.44 | ops/s | 1.3x slower |
| prometheusAdd | 49.57K | ± 1.48K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 64.28 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.47K | ± 229.61 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 331.90 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 209.62 | ops/s | 48x slower |
| openTelemetryInc | 1.32K | ± 199.11 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.24K | ± 54.83 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 111.10 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 29.21 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 139.89 | ops/s | 1.8x slower |
| openTelemetryClassic | 665.19 | ± 13.74 | ops/s | 8.0x slower |
| openTelemetryExponential | 545.39 | ± 12.67 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 541.66K | ± 3.98K | ops/s | **fastest** |
| prometheusWriteToNull | 538.70K | ± 3.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.87K | ± 6.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 502.37K | ± 5.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50239.279    ± 806.438  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1371.459    ± 209.624  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1320.730    ± 199.112  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1236.328     ± 54.828  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49566.935   ± 1484.564  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66209.473   ± 1919.105  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56378.113     ± 64.475  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6202.629    ± 331.899  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.566     ± 64.284  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6472.162    ± 229.605  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.187     ± 13.738  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.392     ± 12.670  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5345.038    ± 111.099  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2922.255    ± 139.894  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.714     ± 29.209  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     502366.905   ± 5269.593  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518866.074   ± 6083.159  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541657.321   ± 3978.638  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538703.965   ± 3965.448  ops/s
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
