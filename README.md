# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-10T06:54:40Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.17K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.84K | ± 364.54 | ops/s | 1.1x slower |
| prometheusAdd | 51.36K | ± 278.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.80K | ± 1.31K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 37.31 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 225.18 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 386.24 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.49K | ± 59.03 | ops/s | 44x slower |
| openTelemetryAdd | 1.39K | ± 213.89 | ops/s | 47x slower |
| openTelemetryInc | 1.34K | ± 157.19 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 159.44 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 54.36 | ops/s | 1.2x slower |
| prometheusNative | 3.26K | ± 98.87 | ops/s | 1.6x slower |
| openTelemetryClassic | 665.90 | ± 31.32 | ops/s | 7.8x slower |
| openTelemetryExponential | 559.57 | ± 18.92 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.03K | ± 9.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.10K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 523.64K | ± 4.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 511.46K | ± 8.33K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48797.682   ± 1310.547  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1390.654    ± 213.887  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1340.880    ± 157.188  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1491.962     ± 59.030  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51360.496    ± 278.640  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65172.325   ± 1050.152  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56843.042    ± 364.538  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6235.734    ± 386.245  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6660.309     ± 37.310  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6480.484    ± 225.181  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.902     ± 31.316  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.574     ± 18.921  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5208.692    ± 159.444  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3263.693     ± 98.867  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4475.844     ± 54.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     523636.809   ± 4166.623  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     511458.863   ± 8330.783  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529103.431   ± 2120.955  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538030.855   ± 9168.381  ops/s
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
