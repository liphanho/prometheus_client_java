# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-14T07:05:28Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.78K | ± 1.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.85K | ± 69.07 | ops/s | 1.2x slower |
| prometheusAdd | 48.21K | ± 321.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.27K | ± 587.63 | ops/s | 1.4x slower |
| simpleclientInc | 6.21K | ± 104.23 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.15K | ± 136.67 | ops/s | 9.7x slower |
| simpleclientAdd | 5.96K | ± 290.02 | ops/s | 10x slower |
| openTelemetryInc | 1.34K | ± 85.88 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.28K | ± 40.25 | ops/s | 47x slower |
| openTelemetryAdd | 1.26K | ± 18.35 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.38K | ± 52.24 | ops/s | **fastest** |
| prometheusClassic | 4.29K | ± 753.45 | ops/s | 1.0x slower |
| prometheusNative | 3.11K | ± 44.97 | ops/s | 1.4x slower |
| openTelemetryClassic | 616.69 | ± 35.74 | ops/s | 7.1x slower |
| openTelemetryExponential | 494.55 | ± 11.51 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 639.53K | ± 6.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.34K | ± 10.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 612.75K | ± 2.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 601.40K | ± 2.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44269.483    ± 587.635  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1264.479     ± 18.346  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1335.867     ± 85.880  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1278.965     ± 40.252  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48207.011    ± 321.476  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59775.472   ± 1290.908  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50853.979     ± 69.074  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5960.159    ± 290.017  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6213.671    ± 104.233  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6151.197    ± 136.671  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        616.694     ± 35.737  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        494.551     ± 11.515  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4286.021    ± 753.447  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3113.109     ± 44.975  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4378.015     ± 52.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     601395.002   ± 2410.345  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     612751.812   ± 2709.507  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630337.262  ± 10414.527  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     639528.320   ± 6535.637  ops/s
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
