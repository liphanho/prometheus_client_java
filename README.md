# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-19T05:41:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.93K | ± 553.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 388.06 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 86.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.37K | ± 309.95 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.67K | ± 41.20 | ops/s | 10x slower |
| simpleclientAdd | 6.55K | ± 17.13 | ops/s | 10x slower |
| simpleclientInc | 6.42K | ± 387.82 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 208.82 | ops/s | 47x slower |
| openTelemetryInc | 1.31K | ± 227.16 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.24K | ± 60.35 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 483.68 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 23.89 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 187.41 | ops/s | 1.9x slower |
| openTelemetryClassic | 695.51 | ± 22.59 | ops/s | 7.9x slower |
| openTelemetryExponential | 561.01 | ± 23.82 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 528.97K | ± 5.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.71K | ± 9.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 500.40K | ± 7.59K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 497.64K | ± 3.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47366.684    ± 309.947  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1412.628    ± 208.816  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1308.447    ± 227.160  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1243.074     ± 60.352  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51614.807     ± 86.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66927.680    ± 553.341  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57054.538    ± 388.060  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6552.907     ± 17.126  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6419.640    ± 387.824  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6672.269     ± 41.201  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.513     ± 22.587  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.012     ± 23.824  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5525.538    ± 483.680  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2939.699    ± 187.407  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4541.802     ± 23.886  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497644.149   ± 3511.968  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     500397.403   ± 7594.132  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524713.857   ± 9369.012  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528972.201   ± 5173.361  ops/s
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
