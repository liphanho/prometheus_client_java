# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-29T09:23:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.06K | ± 6.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.12K | ± 708.97 | ops/s | 1.2x slower |
| prometheusAdd | 61.64K | ± 1.00K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.89K | ± 231.05 | ops/s | 1.3x slower |
| simpleclientInc | 7.99K | ± 45.60 | ops/s | 9.5x slower |
| simpleclientAdd | 7.64K | ± 212.61 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 7.59K | ± 234.44 | ops/s | 10x slower |
| openTelemetryInc | 1.83K | ± 86.91 | ops/s | 42x slower |
| openTelemetryAdd | 1.75K | ± 32.86 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.65K | ± 54.63 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.02K | ± 7.60 | ops/s | **fastest** |
| simpleclient | 5.63K | ± 107.25 | ops/s | 1.2x slower |
| prometheusNative | 3.90K | ± 89.73 | ops/s | 1.8x slower |
| openTelemetryClassic | 796.56 | ± 6.59 | ops/s | 8.8x slower |
| openTelemetryExponential | 664.55 | ± 26.22 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 756.86K | ± 12.17K | ops/s | **fastest** |
| prometheusWriteToNull | 755.16K | ± 3.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 686.39K | ± 13.93K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 686.13K | ± 10.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56893.047    ± 231.046  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1753.691     ± 32.861  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1825.365     ± 86.915  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1652.113     ± 54.628  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61636.304   ± 1002.726  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76059.262   ± 6840.940  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66122.076    ± 708.969  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7642.464    ± 212.615  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7990.883     ± 45.599  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7593.494    ± 234.442  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        796.564      ± 6.594  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        664.551     ± 26.223  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7015.085      ± 7.598  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3897.502     ± 89.728  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5626.095    ± 107.254  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     686392.339  ± 13929.776  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     686134.783  ± 10464.739  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     756860.972  ± 12169.143  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     755159.503   ± 3236.883  ops/s
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
