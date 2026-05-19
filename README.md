# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-19T07:25:52Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.84K | ± 161.88 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.09K | ± 2.54K | ops/s | 1.2x slower |
| prometheusAdd | 48.37K | ± 373.05 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.91K | ± 1.84K | ops/s | 1.4x slower |
| simpleclientInc | 6.26K | ± 36.50 | ops/s | 9.6x slower |
| simpleclientAdd | 6.14K | ± 57.45 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.95K | ± 235.94 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.50K | ± 30.27 | ops/s | 40x slower |
| openTelemetryAdd | 1.29K | ± 11.69 | ops/s | 46x slower |
| openTelemetryInc | 1.27K | ± 75.01 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 424.75 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 30.19 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 87.90 | ops/s | 1.6x slower |
| openTelemetryClassic | 618.75 | ± 18.05 | ops/s | 8.2x slower |
| openTelemetryExponential | 504.66 | ± 12.64 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 613.65K | ± 4.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 607.21K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 585.84K | ± 6.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 574.52K | ± 3.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43911.637   ± 1843.719  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1293.984     ± 11.687  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1274.988     ± 75.006  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1498.744     ± 30.266  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48366.674    ± 373.051  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59837.948    ± 161.878  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50090.968   ± 2535.814  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6144.443     ± 57.451  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6256.973     ± 36.498  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5949.142    ± 235.935  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        618.746     ± 18.054  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        504.664     ± 12.639  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5055.052    ± 424.752  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3089.281     ± 87.903  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4385.996     ± 30.186  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     574515.358   ± 3935.535  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     585835.406   ± 6423.238  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     607212.457   ± 3131.570  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     613648.769   ± 4933.827  ops/s
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
