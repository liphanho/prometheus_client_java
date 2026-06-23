# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-23T07:24:12Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.11K | ± 1.90K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.58K | ± 723.01 | ops/s | 1.1x slower |
| prometheusAdd | 63.27K | ± 759.21 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.67K | ± 1.83K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 8.07K | ± 43.04 | ops/s | 9.4x slower |
| simpleclientInc | 7.84K | ± 299.10 | ops/s | 9.7x slower |
| simpleclientAdd | 7.46K | ± 374.05 | ops/s | 10x slower |
| openTelemetryInc | 1.74K | ± 133.49 | ops/s | 44x slower |
| openTelemetryAdd | 1.71K | ± 160.80 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.62K | ± 92.71 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.79K | ± 129.18 | ops/s | **fastest** |
| prometheusClassic | 5.43K | ± 1.06K | ops/s | 1.1x slower |
| prometheusNative | 3.96K | ± 75.21 | ops/s | 1.5x slower |
| openTelemetryClassic | 765.92 | ± 13.75 | ops/s | 7.6x slower |
| openTelemetryExponential | 658.62 | ± 9.47 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 772.59K | ± 4.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 756.37K | ± 8.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 728.07K | ± 6.92K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 715.98K | ± 5.45K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55672.929   ± 1832.847  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1705.410    ± 160.804  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1743.972    ± 133.490  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1617.482     ± 92.711  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63267.316    ± 759.213  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76106.876   ± 1900.392  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67579.742    ± 723.015  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7460.037    ± 374.052  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7841.011    ± 299.097  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8065.221     ± 43.039  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        765.919     ± 13.750  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        658.621      ± 9.469  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5427.243   ± 1055.959  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3964.712     ± 75.212  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5793.337    ± 129.184  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     715980.388   ± 5448.133  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     728069.491   ± 6916.677  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     756368.143   ± 8175.244  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772589.394   ± 4860.664  ops/s
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
