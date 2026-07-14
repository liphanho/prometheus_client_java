# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T06:08:17Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.69K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.64K | ± 507.18 | ops/s | 1.2x slower |
| prometheusAdd | 48.54K | ± 382.41 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.13K | ± 2.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.22K | ± 162.75 | ops/s | 9.6x slower |
| simpleclientAdd | 6.00K | ± 115.93 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.94K | ± 240.73 | ops/s | 10x slower |
| openTelemetryInc | 1.52K | ± 44.22 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.41K | ± 56.94 | ops/s | 42x slower |
| openTelemetryAdd | 1.40K | ± 84.45 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 155.25 | ops/s | **fastest** |
| prometheusClassic | 4.38K | ± 874.36 | ops/s | 1.0x slower |
| prometheusNative | 3.17K | ± 40.89 | ops/s | 1.4x slower |
| openTelemetryClassic | 613.63 | ± 27.68 | ops/s | 7.3x slower |
| openTelemetryExponential | 512.19 | ± 9.53 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 626.21K | ± 4.62K | ops/s | **fastest** |
| prometheusWriteToNull | 616.51K | ± 80.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 602.78K | ± 5.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 589.51K | ± 5.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43132.491   ± 2028.842  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1396.076     ± 84.450  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1522.504     ± 44.215  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1409.584     ± 56.938  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48537.957    ± 382.412  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59686.359   ± 1282.074  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51636.499    ± 507.176  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6001.862    ± 115.929  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6222.101    ± 162.755  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5942.171    ± 240.726  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        613.635     ± 27.676  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.191      ± 9.527  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4383.771    ± 874.364  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3167.523     ± 40.885  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4469.153    ± 155.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     589511.685   ± 5916.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     602779.768   ± 5455.595  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     626214.248   ± 4616.140  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     616510.878  ± 80352.921  ops/s
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
