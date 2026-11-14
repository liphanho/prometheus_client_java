# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-14T09:57:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.45K | ± 313.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.18K | ± 176.41 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.99K | ± 1.14K | ops/s | 1.0x slower |
| prometheusAdd | 28.20K | ± 193.81 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.42K | ± 301.35 | ops/s | 4.9x slower |
| simpleclientInc | 6.42K | ± 132.80 | ops/s | 4.9x slower |
| simpleclientAdd | 6.10K | ± 329.48 | ops/s | 5.2x slower |
| openTelemetryIncNoLabels | 1.35K | ± 39.14 | ops/s | 23x slower |
| openTelemetryInc | 1.26K | ± 67.89 | ops/s | 25x slower |
| openTelemetryAdd | 1.26K | ± 79.67 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.14K | ± 253.48 | ops/s | **fastest** |
| prometheusClassic | 3.06K | ± 262.72 | ops/s | 1.4x slower |
| prometheusNative | 2.38K | ± 58.66 | ops/s | 1.7x slower |
| openTelemetryClassic | 514.62 | ± 6.13 | ops/s | 8.0x slower |
| openTelemetryExponential | 435.93 | ± 9.31 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 329.02K | ± 2.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 328.14K | ± 2.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 305.86K | ± 1.70K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 304.09K | ± 1.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29993.642   ± 1141.119  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.633     ± 79.669  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.868     ± 67.894  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1346.747     ± 39.144  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28197.209    ± 193.812  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31450.688    ± 313.374  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31180.160    ± 176.410  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6101.982    ± 329.477  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6419.800    ± 132.796  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6424.714    ± 301.350  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        514.616      ± 6.126  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        435.931      ± 9.310  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3055.043    ± 262.716  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2377.029     ± 58.662  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4138.682    ± 253.477  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     304089.235   ± 1160.879  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     305855.141   ± 1701.434  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     328143.445   ± 2110.747  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     329023.278   ± 2510.135  ops/s
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
