# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T04:10:13Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.25K | ± 779.15 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.47K | ± 655.65 | ops/s | 1.1x slower |
| prometheusAdd | 61.50K | ± 942.29 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.85K | ± 837.00 | ops/s | 1.3x slower |
| simpleclientInc | 8.07K | ± 61.42 | ops/s | 9.3x slower |
| simpleclientAdd | 7.70K | ± 159.36 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.64K | ± 292.20 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.74K | ± 181.78 | ops/s | 43x slower |
| openTelemetryAdd | 1.74K | ± 69.90 | ops/s | 43x slower |
| openTelemetryInc | 1.69K | ± 45.54 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.05K | ± 40.66 | ops/s | **fastest** |
| simpleclient | 5.86K | ± 132.46 | ops/s | 1.2x slower |
| prometheusNative | 3.97K | ± 75.01 | ops/s | 1.8x slower |
| openTelemetryClassic | 817.91 | ± 19.64 | ops/s | 8.6x slower |
| openTelemetryExponential | 678.51 | ± 20.85 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 785.15K | ± 4.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 768.52K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 738.53K | ± 7.10K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 725.09K | ± 3.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56850.840    ± 836.998  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1735.171     ± 69.898  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1689.207     ± 45.537  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1742.465    ± 181.778  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61495.883    ± 942.295  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75248.330    ± 779.154  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66466.735    ± 655.649  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7698.762    ± 159.360  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8073.978     ± 61.425  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7641.271    ± 292.201  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        817.907     ± 19.639  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        678.512     ± 20.846  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7052.603     ± 40.658  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3973.197     ± 75.008  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5859.834    ± 132.465  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     725092.618   ± 3480.234  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     738529.344   ± 7100.661  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     768520.472   ± 3550.618  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     785152.425   ± 4418.257  ops/s
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
