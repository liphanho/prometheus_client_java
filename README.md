# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-21T05:24:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.62K | ± 23.22 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.76K | ± 859.93 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.46K | ± 1.01K | ops/s | 1.0x slower |
| prometheusAdd | 28.48K | ± 49.14 | ops/s | 1.1x slower |
| simpleclientInc | 7.03K | ± 42.86 | ops/s | 4.5x slower |
| simpleclientAdd | 6.89K | ± 26.25 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.84K | ± 255.95 | ops/s | 4.6x slower |
| openTelemetryInc | 1.42K | ± 138.91 | ops/s | 22x slower |
| openTelemetryAdd | 1.34K | ± 69.39 | ops/s | 24x slower |
| openTelemetryIncNoLabels | 1.34K | ± 114.00 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.63K | ± 50.52 | ops/s | **fastest** |
| prometheusClassic | 3.14K | ± 206.91 | ops/s | 1.5x slower |
| prometheusNative | 2.22K | ± 199.25 | ops/s | 2.1x slower |
| openTelemetryClassic | 506.67 | ± 24.07 | ops/s | 9.1x slower |
| openTelemetryExponential | 421.71 | ± 14.39 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 341.54K | ± 2.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 341.18K | ± 2.71K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 315.76K | ± 1.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 314.40K | ± 2.14K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30763.671    ± 859.932  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1337.379     ± 69.386  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1424.741    ± 138.910  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1336.898    ± 114.002  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28476.738     ± 49.143  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31620.740     ± 23.224  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30456.265   ± 1007.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6887.212     ± 26.252  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7032.315     ± 42.865  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6837.067    ± 255.948  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        506.674     ± 24.069  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        421.710     ± 14.392  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3138.054    ± 206.910  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2221.750    ± 199.252  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4631.228     ± 50.515  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     314395.582   ± 2143.218  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     315762.645   ± 1435.691  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     341178.387   ± 2714.234  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     341537.343   ± 2309.975  ops/s
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
