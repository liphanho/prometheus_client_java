# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-09T09:49:34Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.94K | ± 139.43 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.47K | ± 2.48K | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 101.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.44K | ± 1.37K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 59.29 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.44K | ± 126.80 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 338.76 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 202.39 | ops/s | 47x slower |
| openTelemetryInc | 1.26K | ± 7.32 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 36.72 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 30.31 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 31.48 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 139.06 | ops/s | 1.7x slower |
| openTelemetryClassic | 687.96 | ± 30.79 | ops/s | 7.6x slower |
| openTelemetryExponential | 581.36 | ± 13.19 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.66K | ± 7.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 511.78K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.26K | ± 3.05K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 500.80K | ± 10.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49444.685   ± 1374.284  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1414.371    ± 202.389  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1260.563      ± 7.317  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1229.241     ± 36.717  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51278.999    ± 101.364  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65938.453    ± 139.428  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55469.488   ± 2482.619  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6251.628    ± 338.762  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6658.637     ± 59.292  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6438.460    ± 126.802  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.961     ± 30.789  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        581.360     ± 13.188  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5241.251     ± 30.308  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3024.571    ± 139.055  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4466.741     ± 31.482  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505263.276   ± 3050.001  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     500797.046  ± 10501.519  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     511776.507   ± 3646.688  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530661.832   ± 7497.493  ops/s
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
