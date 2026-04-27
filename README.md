# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-27T06:41:25Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.06K | ± 818.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.28K | ± 254.93 | ops/s | 1.1x slower |
| prometheusAdd | 50.62K | ± 1.29K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.93K | ± 1.64K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.62K | ± 20.29 | ops/s | 9.5x slower |
| simpleclientInc | 6.58K | ± 28.76 | ops/s | 9.6x slower |
| simpleclientAdd | 6.36K | ± 194.87 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.57K | ± 273.93 | ops/s | 40x slower |
| openTelemetryInc | 1.45K | ± 119.63 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.24K | ± 31.88 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 33.74 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 32.63 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 97.34 | ops/s | 1.7x slower |
| openTelemetryClassic | 686.12 | ± 19.82 | ops/s | 7.6x slower |
| openTelemetryExponential | 552.12 | ± 12.32 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.82K | ± 4.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 537.81K | ± 3.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.37K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.87K | ± 6.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47927.222   ± 1636.781  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1573.672    ± 273.927  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1452.577    ± 119.628  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1238.409     ± 31.877  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50624.372   ± 1293.532  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63064.594    ± 818.025  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56283.747    ± 254.930  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6359.132    ± 194.867  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.802     ± 28.765  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6617.437     ± 20.290  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.120     ± 19.819  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.122     ± 12.324  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5248.052     ± 33.739  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3074.639     ± 97.337  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.908     ± 32.628  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509869.048   ± 6117.757  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516369.783   ± 4504.748  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     537807.508   ± 3868.402  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540823.214   ± 4682.312  ops/s
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
