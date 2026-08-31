# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-31T09:27:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.56K | ± 1.50K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.24K | ± 494.39 | ops/s | 1.1x slower |
| prometheusAdd | 48.17K | ± 480.66 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.89K | ± 557.62 | ops/s | 1.3x slower |
| simpleclientInc | 6.27K | ± 162.01 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.07K | ± 175.77 | ops/s | 9.6x slower |
| simpleclientAdd | 6.00K | ± 268.44 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.55K | ± 33.34 | ops/s | 38x slower |
| openTelemetryInc | 1.42K | ± 109.06 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.33K | ± 35.20 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.99K | ± 423.24 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 52.94 | ops/s | 1.1x slower |
| prometheusNative | 3.08K | ± 91.49 | ops/s | 1.6x slower |
| openTelemetryClassic | 607.98 | ± 36.75 | ops/s | 8.2x slower |
| openTelemetryExponential | 517.35 | ± 10.68 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 645.62K | ± 5.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 629.29K | ± 3.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 607.86K | ± 3.83K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 594.99K | ± 3.02K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44891.646    ± 557.623  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1546.388     ± 33.342  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1421.261    ± 109.058  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1332.375     ± 35.200  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48174.076    ± 480.657  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58555.442   ± 1496.490  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51242.686    ± 494.388  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5999.112    ± 268.441  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6265.369    ± 162.010  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6072.942    ± 175.774  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        607.984     ± 36.749  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.355     ± 10.675  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4990.412    ± 423.245  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3079.003     ± 91.494  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.510     ± 52.942  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     594985.438   ± 3024.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     607860.229   ± 3825.655  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     629292.518   ± 3831.735  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     645622.194   ± 5793.397  ops/s
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
