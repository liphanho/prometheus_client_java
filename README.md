# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-04T08:16:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.16K | ± 112.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.84K | ± 272.86 | ops/s | 1.1x slower |
| prometheusAdd | 63.71K | ± 871.32 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.40K | ± 2.68K | ops/s | 1.4x slower |
| simpleclientAdd | 7.99K | ± 10.71 | ops/s | 9.5x slower |
| simpleclientInc | 7.81K | ± 280.82 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.47K | ± 21.42 | ops/s | 10x slower |
| openTelemetryAdd | 1.91K | ± 101.05 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.83K | ± 126.09 | ops/s | 42x slower |
| openTelemetryInc | 1.74K | ± 76.11 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.86K | ± 248.46 | ops/s | **fastest** |
| simpleclient | 5.83K | ± 137.90 | ops/s | 1.2x slower |
| prometheusNative | 4.03K | ± 129.89 | ops/s | 1.7x slower |
| openTelemetryClassic | 812.25 | ± 12.46 | ops/s | 8.5x slower |
| openTelemetryExponential | 665.71 | ± 22.45 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 764.49K | ± 10.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 748.56K | ± 6.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 724.71K | ± 11.40K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 717.22K | ± 4.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55403.222   ± 2677.740  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1913.363    ± 101.050  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1742.234     ± 76.108  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1828.819    ± 126.088  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63710.965    ± 871.320  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76157.940    ± 112.120  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66839.084    ± 272.858  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7985.895     ± 10.712  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7812.016    ± 280.823  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7469.879     ± 21.419  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        812.255     ± 12.462  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        665.705     ± 22.454  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6863.847    ± 248.465  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4031.873    ± 129.892  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5826.770    ± 137.896  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     717218.701   ± 4246.202  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     724706.762  ± 11398.819  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     748559.044   ± 6137.586  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     764492.720  ± 10156.741  ops/s
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
