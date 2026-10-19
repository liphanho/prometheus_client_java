# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-19T08:39:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.24K | ± 592.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 178.76 | ops/s | 1.2x slower |
| prometheusAdd | 51.33K | ± 220.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.28K | ± 1.48K | ops/s | 1.4x slower |
| simpleclientAdd | 6.48K | ± 19.49 | ops/s | 10x slower |
| simpleclientInc | 6.40K | ± 136.30 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 179.63 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 197.37 | ops/s | 45x slower |
| openTelemetryInc | 1.28K | ± 86.06 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.24K | ± 104.38 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.58K | ± 16.77 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 16.60 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 163.04 | ops/s | 1.9x slower |
| openTelemetryClassic | 677.54 | ± 14.89 | ops/s | 8.2x slower |
| openTelemetryExponential | 557.11 | ± 10.99 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 518.17K | ± 4.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 511.37K | ± 3.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 496.06K | ± 4.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 493.51K | ± 5.63K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48278.924   ± 1483.236  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1471.557    ± 197.374  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1282.891     ± 86.062  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1239.106    ± 104.380  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51326.394    ± 220.393  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66240.866    ± 592.331  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56388.423    ± 178.762  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6476.092     ± 19.494  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6403.990    ± 136.301  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6368.570    ± 179.629  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.537     ± 14.888  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.111     ± 10.991  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5584.519     ± 16.771  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2996.824    ± 163.043  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.592     ± 16.603  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     493512.026   ± 5626.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     496061.391   ± 4242.560  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     511374.617   ± 3671.357  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     518174.227   ± 4938.968  ops/s
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
