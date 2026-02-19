# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-19T05:38:35Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.60K | ± 538.64 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 946.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.81K | ± 108.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.11K | ± 1.76K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 30.23 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.58K | ± 109.72 | ops/s | 10x slower |
| simpleclientAdd | 6.53K | ± 13.69 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 179.41 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.31K | ± 150.89 | ops/s | 51x slower |
| openTelemetryAdd | 1.24K | ± 20.69 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 47.15 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 49.16 | ops/s | 1.2x slower |
| prometheusNative | 3.18K | ± 65.16 | ops/s | 1.7x slower |
| openTelemetryClassic | 657.68 | ± 5.97 | ops/s | 8.0x slower |
| openTelemetryExponential | 535.61 | ± 16.64 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.84K | ± 3.99K | ops/s | **fastest** |
| openMetricsWriteToNull | 514.80K | ± 8.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.19K | ± 6.48K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 513.80K | ± 16.22K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48110.903   ± 1761.213  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.570     ± 20.688  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.852    ± 179.412  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1307.906    ± 150.886  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51812.027    ± 108.489  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66595.337    ± 538.639  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56238.053    ± 946.936  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6529.375     ± 13.686  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6769.845     ± 30.228  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6577.475    ± 109.716  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.681      ± 5.973  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.612     ± 16.641  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5279.723     ± 47.149  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3175.681     ± 65.158  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4532.312     ± 49.158  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514193.776   ± 6481.497  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514795.718   ± 8766.199  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513799.720  ± 16224.637  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532844.345   ± 3994.312  ops/s
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
