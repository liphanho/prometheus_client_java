# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-02T10:13:31Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.71K | ± 917.47 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.82K | ± 1.36K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 61.65K | ± 1.07K | ops/s | 1.1x slower |
| prometheusAdd | 59.02K | ± 2.22K | ops/s | 1.1x slower |
| simpleclientInc | 10.89K | ± 104.54 | ops/s | 6.1x slower |
| simpleclientNoLabelsInc | 10.70K | ± 293.14 | ops/s | 6.2x slower |
| simpleclientAdd | 10.48K | ± 180.64 | ops/s | 6.4x slower |
| openTelemetryIncNoLabels | 1.85K | ± 283.39 | ops/s | 36x slower |
| openTelemetryAdd | 1.85K | ± 252.18 | ops/s | 36x slower |
| openTelemetryInc | 1.79K | ± 31.96 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.07K | ± 118.54 | ops/s | **fastest** |
| simpleclient | 6.76K | ± 122.83 | ops/s | 1.0x slower |
| prometheusNative | 4.68K | ± 446.55 | ops/s | 1.5x slower |
| openTelemetryClassic | 874.69 | ± 25.20 | ops/s | 8.1x slower |
| openTelemetryExponential | 700.20 | ± 77.64 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 781.46K | ± 33.15K | ops/s | **fastest** |
| prometheusWriteToNull | 754.08K | ± 6.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 748.18K | ± 34.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 701.47K | ± 61.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61646.466   ± 1065.127  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1848.656    ± 252.183  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1789.767     ± 31.965  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1849.040    ± 283.392  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59015.106   ± 2220.063  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66711.151    ± 917.473  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65822.575   ± 1363.549  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10484.137    ± 180.640  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10887.624    ± 104.539  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10704.805    ± 293.142  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        874.688     ± 25.196  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        700.204     ± 77.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7072.055    ± 118.541  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4678.739    ± 446.550  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6763.308    ± 122.828  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     701474.242  ± 61633.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     748175.319  ± 34965.713  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     781455.207  ± 33147.830  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     754080.866   ± 6719.313  ops/s
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
