# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-04T05:36:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.92K | ± 1.78K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.16K | ± 1.12K | ops/s | 1.2x slower |
| prometheusAdd | 51.41K | ± 176.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.15K | ± 1.15K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 29.46 | ops/s | 9.9x slower |
| simpleclientAdd | 6.35K | ± 182.25 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 229.02 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.32K | ± 151.36 | ops/s | 50x slower |
| openTelemetryAdd | 1.26K | ± 43.78 | ops/s | 52x slower |
| openTelemetryInc | 1.23K | ± 17.95 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 36.98 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 189.25 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 85.93 | ops/s | 1.7x slower |
| openTelemetryClassic | 686.94 | ± 48.42 | ops/s | 7.6x slower |
| openTelemetryExponential | 540.74 | ± 15.02 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.87K | ± 5.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.37K | ± 7.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.22K | ± 8.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.94K | ± 5.67K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48148.563   ± 1151.967  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1259.910     ± 43.777  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1233.529     ± 17.955  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.235    ± 151.361  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51407.914    ± 176.680  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65917.411   ± 1782.088  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56163.016   ± 1120.831  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6351.509    ± 182.246  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6678.332     ± 29.461  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.075    ± 229.016  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.940     ± 48.419  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.738     ± 15.021  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5214.717     ± 36.984  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3093.200     ± 85.935  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4340.382    ± 189.246  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509937.635   ± 5669.198  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515217.550   ± 8765.165  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527367.319   ± 7042.660  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539866.480   ± 5872.243  ops/s
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
