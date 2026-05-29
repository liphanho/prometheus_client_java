# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-29T07:31:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.91K | ± 84.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 408.32 | ops/s | 1.2x slower |
| prometheusAdd | 48.34K | ± 844.85 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.11K | ± 142.77 | ops/s | 1.4x slower |
| simpleclientInc | 6.26K | ± 153.25 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.06K | ± 255.19 | ops/s | 9.9x slower |
| simpleclientAdd | 5.93K | ± 159.20 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 69.81 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.39K | ± 189.70 | ops/s | 43x slower |
| openTelemetryAdd | 1.38K | ± 63.32 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.44K | ± 785.07 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 91.03 | ops/s | 1.0x slower |
| prometheusNative | 3.07K | ± 53.25 | ops/s | 1.4x slower |
| openTelemetryClassic | 620.81 | ± 25.12 | ops/s | 7.2x slower |
| openTelemetryExponential | 508.21 | ± 2.24 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 640.62K | ± 6.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 631.93K | ± 2.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 609.34K | ± 9.64K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 592.98K | ± 9.58K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44114.761    ± 142.768  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1378.298     ± 63.315  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1421.888     ± 69.814  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1385.825    ± 189.704  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48336.366    ± 844.845  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59910.771     ± 84.117  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51192.678    ± 408.320  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5925.854    ± 159.202  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6258.683    ± 153.250  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6058.780    ± 255.192  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        620.813     ± 25.115  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        508.208      ± 2.243  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4441.240    ± 785.069  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3066.919     ± 53.252  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4353.119     ± 91.029  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     592977.209   ± 9576.744  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     609336.932   ± 9642.535  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     631925.328   ± 2587.469  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     640617.581   ± 6504.754  ops/s
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
