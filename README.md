# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-11T08:06:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.73K | ± 1.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.01K | ± 732.78 | ops/s | 1.2x slower |
| prometheusAdd | 48.14K | ± 319.64 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.59K | ± 5.76K | ops/s | 1.5x slower |
| simpleclientInc | 6.17K | ± 103.64 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.11K | ± 233.25 | ops/s | 9.8x slower |
| simpleclientAdd | 6.01K | ± 178.84 | ops/s | 9.9x slower |
| openTelemetryInc | 1.54K | ± 26.79 | ops/s | 39x slower |
| openTelemetryAdd | 1.49K | ± 67.79 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.43K | ± 110.60 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 472.65 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 139.31 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 115.32 | ops/s | 1.7x slower |
| openTelemetryClassic | 657.66 | ± 5.90 | ops/s | 8.0x slower |
| openTelemetryExponential | 522.86 | ± 10.09 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 634.10K | ± 6.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 614.53K | ± 9.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 604.25K | ± 10.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 591.02K | ± 3.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40588.780   ± 5760.438  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1494.810     ± 67.789  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1541.225     ± 26.790  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1432.425    ± 110.600  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48136.043    ± 319.636  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59729.110   ± 1125.389  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51012.536    ± 732.784  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6010.851    ± 178.838  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6170.704    ± 103.637  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6110.418    ± 233.251  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.662      ± 5.902  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.864     ± 10.089  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5275.240    ± 472.646  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3102.656    ± 115.315  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.237    ± 139.310  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     591023.151   ± 3443.527  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     604253.207  ± 10302.316  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     614527.118   ± 9532.269  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     634095.887   ± 6382.678  ops/s
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
