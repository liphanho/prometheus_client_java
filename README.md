# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-22T08:27:56Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.75K | ± 1.61K | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.91K | ± 731.89 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 58.63K | ± 716.05 | ops/s | 1.1x slower |
| prometheusAdd | 58.23K | ± 3.57K | ops/s | 1.1x slower |
| simpleclientInc | 10.24K | ± 58.22 | ops/s | 6.4x slower |
| simpleclientAdd | 10.21K | ± 296.02 | ops/s | 6.4x slower |
| simpleclientNoLabelsInc | 10.17K | ± 193.84 | ops/s | 6.5x slower |
| openTelemetryAdd | 2.33K | ± 419.30 | ops/s | 28x slower |
| openTelemetryInc | 2.03K | ± 238.51 | ops/s | 32x slower |
| openTelemetryIncNoLabels | 2.00K | ± 224.97 | ops/s | 33x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.34K | ± 262.10 | ops/s | **fastest** |
| simpleclient | 6.74K | ± 125.53 | ops/s | 1.1x slower |
| prometheusNative | 5.17K | ± 374.30 | ops/s | 1.4x slower |
| openTelemetryClassic | 851.05 | ± 14.82 | ops/s | 8.6x slower |
| openTelemetryExponential | 688.16 | ± 13.98 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 769.84K | ± 59.54K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 729.45K | ± 38.50K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 713.49K | ± 43.03K | ops/s | 1.1x slower |
| prometheusWriteToNull | 710.63K | ± 17.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      58630.379    ± 716.049  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2330.863    ± 419.300  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2034.906    ± 238.512  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2004.208    ± 224.971  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58234.691   ± 3569.397  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65745.348   ± 1614.251  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63906.879    ± 731.890  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10206.936    ± 296.019  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10241.651     ± 58.222  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10168.705    ± 193.841  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        851.053     ± 14.816  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        688.163     ± 13.975  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7342.739    ± 262.101  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5166.571    ± 374.297  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6737.235    ± 125.528  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     729452.691  ± 38495.889  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     713490.089  ± 43026.656  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     769839.022  ± 59539.977  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     710625.331  ± 17507.886  ops/s
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
