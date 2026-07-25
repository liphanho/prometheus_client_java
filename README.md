# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-25T06:33:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 36.03K | ± 638.61 | ops/s | **fastest** |
| codahaleIncNoLabels | 36.00K | ± 2.23K | ops/s | 1.0x slower |
| prometheusInc | 35.64K | ± 259.58 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 34.89K | ± 1.56K | ops/s | 1.0x slower |
| simpleclientNoLabelsInc | 9.20K | ± 151.82 | ops/s | 3.9x slower |
| simpleclientInc | 9.18K | ± 110.77 | ops/s | 3.9x slower |
| simpleclientAdd | 9.04K | ± 128.82 | ops/s | 4.0x slower |
| openTelemetryAdd | 900.44 | ± 22.46 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 871.55 | ± 59.13 | ops/s | 41x slower |
| openTelemetryInc | 867.91 | ± 9.20 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.83K | ± 149.39 | ops/s | **fastest** |
| prometheusClassic | 2.52K | ± 255.06 | ops/s | 2.3x slower |
| prometheusNative | 1.91K | ± 232.13 | ops/s | 3.1x slower |
| openTelemetryClassic | 371.86 | ± 38.26 | ops/s | 16x slower |
| openTelemetryExponential | 349.95 | ± 19.75 | ops/s | 17x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 348.10K | ± 2.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 344.90K | ± 4.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 324.92K | ± 2.13K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 320.36K | ± 1.58K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      36004.335   ± 2231.601  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        900.445     ± 22.458  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        867.906      ± 9.195  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        871.554     ± 59.125  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36028.520    ± 638.611  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35643.066    ± 259.580  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      34886.657   ± 1561.608  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9044.507    ± 128.816  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9177.408    ± 110.771  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9204.736    ± 151.817  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        371.865     ± 38.259  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        349.951     ± 19.755  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2519.669    ± 255.058  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1906.685    ± 232.129  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5834.253    ± 149.391  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     320363.638   ± 1583.839  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     324915.621   ± 2130.765  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     344901.397   ± 4824.106  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     348104.611   ± 2609.228  ops/s
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
