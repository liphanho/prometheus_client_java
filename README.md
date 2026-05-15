# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-15T07:12:06Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.47K | ± 680.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 785.68 | ops/s | 1.2x slower |
| prometheusAdd | 51.25K | ± 320.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.07K | ± 137.58 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.52K | ± 150.10 | ops/s | 10x slower |
| simpleclientInc | 6.38K | ± 87.95 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 232.59 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 211.45 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.35K | ± 220.83 | ops/s | 49x slower |
| openTelemetryInc | 1.24K | ± 16.93 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 96.96 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 50.20 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 106.01 | ops/s | 1.7x slower |
| openTelemetryClassic | 695.00 | ± 23.80 | ops/s | 7.6x slower |
| openTelemetryExponential | 567.42 | ± 24.91 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.04K | ± 2.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.12K | ± 6.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.84K | ± 3.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.86K | ± 8.38K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47074.700    ± 137.581  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.766    ± 211.449  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1236.943     ± 16.930  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1349.952    ± 220.834  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51253.230    ± 320.178  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66467.999    ± 680.632  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56802.546    ± 785.676  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6175.635    ± 232.592  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6375.028     ± 87.949  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6518.606    ± 150.097  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.003     ± 23.796  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.423     ± 24.910  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5256.393     ± 96.955  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3053.874    ± 106.008  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4484.853     ± 50.203  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506859.240   ± 8382.624  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512838.334   ± 3334.483  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524116.630   ± 6849.523  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527041.963   ± 2190.674  ops/s
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
