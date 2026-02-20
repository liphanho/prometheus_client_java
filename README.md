# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-20T05:33:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.72K | ± 1.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 433.66 | ops/s | 1.1x slower |
| prometheusAdd | 50.90K | ± 986.34 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.07K | ± 1.32K | ops/s | 1.3x slower |
| simpleclientInc | 6.80K | ± 12.87 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.45K | ± 205.05 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 260.22 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 302.02 | ops/s | 41x slower |
| openTelemetryInc | 1.35K | ± 205.95 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.28K | ± 174.87 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 307.86 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 23.08 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 196.20 | ops/s | 1.8x slower |
| openTelemetryClassic | 702.69 | ± 37.48 | ops/s | 7.7x slower |
| openTelemetryExponential | 553.55 | ± 3.06 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.03K | ± 7.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 552.47K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.00K | ± 1.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.50K | ± 5.96K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50072.839   ± 1322.351  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1564.800    ± 302.022  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1353.911    ± 205.952  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1284.685    ± 174.872  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50899.741    ± 986.338  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64718.376   ± 1552.788  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57237.774    ± 433.664  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6430.087    ± 260.223  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6796.883     ± 12.873  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6446.105    ± 205.054  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.686     ± 37.478  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.554      ± 3.065  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5391.200    ± 307.856  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3019.860    ± 196.197  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4556.107     ± 23.081  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524500.463   ± 5955.793  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534995.991   ± 1287.073  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     552469.017   ± 3546.413  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559031.692   ± 7952.195  ops/s
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
