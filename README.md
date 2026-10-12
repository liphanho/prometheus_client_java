# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-12T10:00:13Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.79K | ± 693.89 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.04K | ± 1.49K | ops/s | 1.2x slower |
| prometheusAdd | 62.94K | ± 1.09K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.94K | ± 1.46K | ops/s | 1.4x slower |
| simpleclientInc | 7.82K | ± 41.11 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.81K | ± 263.08 | ops/s | 10.0x slower |
| simpleclientAdd | 7.61K | ± 334.42 | ops/s | 10x slower |
| openTelemetryAdd | 1.91K | ± 141.70 | ops/s | 41x slower |
| openTelemetryInc | 1.82K | ± 126.55 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.74K | ± 112.98 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.24K | ± 64.32 | ops/s | **fastest** |
| simpleclient | 5.71K | ± 34.73 | ops/s | 1.3x slower |
| prometheusNative | 4.18K | ± 75.29 | ops/s | 1.7x slower |
| openTelemetryClassic | 780.26 | ± 8.66 | ops/s | 9.3x slower |
| openTelemetryExponential | 709.11 | ± 18.60 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 760.68K | ± 7.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 748.15K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 727.52K | ± 4.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 713.87K | ± 2.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55940.380   ± 1463.250  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1910.977    ± 141.703  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1823.133    ± 126.552  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1744.465    ± 112.983  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62935.584   ± 1090.159  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77788.033    ± 693.894  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66036.620   ± 1488.561  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7610.057    ± 334.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7821.691     ± 41.115  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7813.888    ± 263.083  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.261      ± 8.665  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        709.108     ± 18.598  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7239.574     ± 64.321  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4178.749     ± 75.287  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5706.550     ± 34.732  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     713865.002   ± 2854.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     727515.743   ± 4914.709  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     748150.379   ± 5010.956  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     760675.211   ± 7067.974  ops/s
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
