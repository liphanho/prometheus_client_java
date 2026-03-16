# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-16T05:57:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.28K | ± 645.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.34K | ± 953.91 | ops/s | 1.2x slower |
| prometheusAdd | 51.08K | ± 606.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.74K | ± 1.86K | ops/s | 1.4x slower |
| simpleclientInc | 6.79K | ± 18.32 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.50K | ± 150.24 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 152.33 | ops/s | 11x slower |
| openTelemetryAdd | 1.53K | ± 246.65 | ops/s | 43x slower |
| openTelemetryInc | 1.32K | ± 135.26 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.31K | ± 169.37 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.18K | ± 172.28 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 40.90 | ops/s | 1.1x slower |
| prometheusNative | 3.06K | ± 90.31 | ops/s | 1.7x slower |
| openTelemetryClassic | 717.71 | ± 7.31 | ops/s | 7.2x slower |
| openTelemetryExponential | 522.29 | ± 31.05 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 515.43K | ± 3.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.69K | ± 8.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 500.05K | ± 4.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 497.93K | ± 3.38K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48735.998   ± 1857.545  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1530.335    ± 246.652  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.367    ± 135.264  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.606    ± 169.368  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51075.177    ± 606.774  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66284.367    ± 645.592  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56344.321    ± 953.912  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6117.333    ± 152.327  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6792.405     ± 18.317  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6497.902    ± 150.242  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.713      ± 7.315  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.287     ± 31.047  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5176.656    ± 172.284  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3059.769     ± 90.313  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4526.426     ± 40.901  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497933.592   ± 3383.893  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     500054.438   ± 4894.985  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512694.735   ± 8243.967  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515431.644   ± 3071.434  ops/s
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
