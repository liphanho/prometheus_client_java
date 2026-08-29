# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-29T09:57:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 29.81K | ± 532.89 | ops/s | **fastest** |
| prometheusInc | 29.80K | ± 220.16 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 29.64K | ± 489.45 | ops/s | 1.0x slower |
| prometheusAdd | 29.30K | ± 157.06 | ops/s | 1.0x slower |
| simpleclientNoLabelsInc | 7.53K | ± 48.80 | ops/s | 4.0x slower |
| simpleclientInc | 7.50K | ± 88.55 | ops/s | 4.0x slower |
| simpleclientAdd | 7.38K | ± 185.04 | ops/s | 4.0x slower |
| openTelemetryIncNoLabels | 1.27K | ± 76.21 | ops/s | 24x slower |
| openTelemetryAdd | 1.20K | ± 119.21 | ops/s | 25x slower |
| openTelemetryInc | 1.12K | ± 107.05 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.86K | ± 63.46 | ops/s | **fastest** |
| prometheusClassic | 2.95K | ± 342.42 | ops/s | 1.6x slower |
| prometheusNative | 2.15K | ± 111.26 | ops/s | 2.3x slower |
| openTelemetryClassic | 422.99 | ± 23.53 | ops/s | 11x slower |
| openTelemetryExponential | 312.32 | ± 16.72 | ops/s | 16x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 318.49K | ± 1.69K | ops/s | **fastest** |
| prometheusWriteToNull | 314.14K | ± 3.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 294.12K | ± 3.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 292.50K | ± 1.35K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29807.953    ± 532.890  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1197.503    ± 119.212  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1121.461    ± 107.047  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1267.186     ± 76.206  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29299.184    ± 157.060  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29799.074    ± 220.157  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29641.656    ± 489.450  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7384.278    ± 185.037  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7497.339     ± 88.554  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7525.096     ± 48.805  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        422.992     ± 23.534  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        312.315     ± 16.722  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2951.849    ± 342.420  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2147.435    ± 111.260  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4857.996     ± 63.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     292501.530   ± 1352.330  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     294115.069   ± 3250.992  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     318492.328   ± 1685.908  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     314139.546   ± 3988.335  ops/s
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
