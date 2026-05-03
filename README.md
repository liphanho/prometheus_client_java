# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-03T06:48:05Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.04K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.09K | ± 1.24K | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 689.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.34K | ± 126.41 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 71.53 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.42K | ± 239.66 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 136.61 | ops/s | 11x slower |
| openTelemetryAdd | 1.74K | ± 63.87 | ops/s | 37x slower |
| openTelemetryIncNoLabels | 1.31K | ± 162.75 | ops/s | 49x slower |
| openTelemetryInc | 1.25K | ± 46.94 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 249.46 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 67.21 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 72.11 | ops/s | 1.7x slower |
| openTelemetryClassic | 703.34 | ± 6.00 | ops/s | 7.6x slower |
| openTelemetryExponential | 582.64 | ± 7.74 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.14K | ± 6.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 518.79K | ± 7.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.44K | ± 4.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 496.95K | ± 4.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50340.878    ± 126.411  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1744.968     ± 63.866  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1246.634     ± 46.942  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.726    ± 162.749  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51166.801    ± 689.620  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65040.017   ± 1211.669  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56086.623   ± 1235.177  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.075    ± 136.606  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6659.749     ± 71.529  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6418.609    ± 239.665  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.335      ± 6.002  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        582.644      ± 7.737  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5337.001    ± 249.456  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3132.751     ± 72.108  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4391.063     ± 67.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     496949.210   ± 4436.159  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510436.402   ± 4838.717  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     518794.646   ± 7475.079  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533135.959   ± 6685.111  ops/s
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
