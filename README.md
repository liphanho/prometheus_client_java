# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-28T09:14:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.10K | ± 52.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.11K | ± 480.13 | ops/s | 1.2x slower |
| prometheusAdd | 48.84K | ± 693.52 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.81K | ± 1.84K | ops/s | 1.4x slower |
| simpleclientInc | 6.30K | ± 40.89 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 5.99K | ± 236.95 | ops/s | 9.9x slower |
| simpleclientAdd | 5.96K | ± 308.47 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.45K | ± 84.11 | ops/s | 41x slower |
| openTelemetryAdd | 1.38K | ± 74.28 | ops/s | 43x slower |
| openTelemetryInc | 1.37K | ± 106.49 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.32K | ± 478.69 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 77.76 | ops/s | 1.2x slower |
| prometheusNative | 3.11K | ± 104.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 639.82 | ± 9.82 | ops/s | 8.3x slower |
| openTelemetryExponential | 523.96 | ± 33.40 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.26K | ± 6.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 632.23K | ± 3.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 614.82K | ± 3.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 595.27K | ± 4.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42807.796   ± 1836.500  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1380.326     ± 74.282  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.621    ± 106.491  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1453.482     ± 84.106  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48842.863    ± 693.516  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59097.500     ± 52.728  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51108.571    ± 480.133  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5958.770    ± 308.473  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6296.210     ± 40.889  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5985.040    ± 236.947  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        639.815      ± 9.821  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.957     ± 33.399  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5322.893    ± 478.688  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3107.490    ± 104.084  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4317.105     ± 77.763  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     595267.360   ± 4594.673  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     614817.625   ± 3573.080  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     632233.684   ± 3885.051  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643264.427   ± 6209.001  ops/s
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
