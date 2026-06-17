# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-17T08:27:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.32K | ± 855.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 554.80 | ops/s | 1.2x slower |
| prometheusAdd | 51.53K | ± 244.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.58K | ± 438.50 | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 10.23 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 177.48 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 33.26 | ops/s | 10x slower |
| openTelemetryInc | 1.39K | ± 145.35 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.26K | ± 13.06 | ops/s | 53x slower |
| openTelemetryAdd | 1.25K | ± 29.92 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 68.63 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 136.15 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 172.26 | ops/s | 1.7x slower |
| openTelemetryClassic | 652.80 | ± 18.58 | ops/s | 8.0x slower |
| openTelemetryExponential | 558.62 | ± 25.62 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 515.26K | ± 7.44K | ops/s | **fastest** |
| prometheusWriteToNull | 508.81K | ± 9.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.42K | ± 9.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 489.04K | ± 7.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47580.278    ± 438.498  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1245.822     ± 29.917  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1387.905    ± 145.346  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1260.712     ± 13.064  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51526.494    ± 244.488  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66324.584    ± 855.292  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56382.976    ± 554.796  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6456.383     ± 33.260  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6674.579     ± 10.231  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.667    ± 177.483  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.802     ± 18.578  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.623     ± 25.621  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5219.886     ± 68.625  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3050.366    ± 172.255  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4336.060    ± 136.152  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489038.026   ± 7656.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492416.044   ± 9443.693  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515262.415   ± 7443.369  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508811.973   ± 9255.263  ops/s
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
