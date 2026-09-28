# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-28T09:35:47Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.45K | ± 382.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.63K | ± 244.39 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 97.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.16K | ± 2.13K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 12.42 | ops/s | 9.9x slower |
| simpleclientInc | 6.57K | ± 206.44 | ops/s | 10.0x slower |
| simpleclientAdd | 6.21K | ± 207.25 | ops/s | 11x slower |
| openTelemetryAdd | 1.46K | ± 281.91 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.25K | ± 85.09 | ops/s | 52x slower |
| openTelemetryInc | 1.22K | ± 51.96 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.10K | ± 287.95 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 44.71 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 142.81 | ops/s | 1.8x slower |
| openTelemetryClassic | 665.52 | ± 43.40 | ops/s | 7.7x slower |
| openTelemetryExponential | 566.01 | ± 37.47 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.24K | ± 5.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 516.77K | ± 7.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.62K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 498.02K | ± 4.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48155.902   ± 2125.750  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1461.197    ± 281.906  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1217.434     ± 51.959  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1250.281     ± 85.093  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51449.545     ± 97.052  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65448.975    ± 382.524  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56629.877    ± 244.393  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6214.246    ± 207.253  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6573.875    ± 206.441  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6604.248     ± 12.419  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.515     ± 43.402  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.015     ± 37.467  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5101.822    ± 287.954  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2900.576    ± 142.813  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.428     ± 44.711  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     498019.072   ± 4834.589  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514621.963   ± 6131.268  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     516772.988   ± 7161.848  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526244.416   ± 5355.228  ops/s
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
