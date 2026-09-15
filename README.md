# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T08:33:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.81K | ± 401.62 | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.82K | ± 829.32 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 63.66K | ± 2.73K | ops/s | 1.0x slower |
| prometheusAdd | 57.15K | ± 3.17K | ops/s | 1.2x slower |
| simpleclientInc | 10.30K | ± 331.42 | ops/s | 6.4x slower |
| simpleclientNoLabelsInc | 10.05K | ± 95.91 | ops/s | 6.5x slower |
| simpleclientAdd | 9.97K | ± 299.08 | ops/s | 6.6x slower |
| openTelemetryAdd | 2.09K | ± 313.09 | ops/s | 31x slower |
| openTelemetryInc | 1.99K | ± 235.15 | ops/s | 33x slower |
| openTelemetryIncNoLabels | 1.97K | ± 219.63 | ops/s | 33x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.41K | ± 140.59 | ops/s | **fastest** |
| simpleclient | 7.00K | ± 271.08 | ops/s | 1.1x slower |
| prometheusNative | 5.47K | ± 77.33 | ops/s | 1.4x slower |
| openTelemetryClassic | 866.24 | ± 31.60 | ops/s | 8.6x slower |
| openTelemetryExponential | 688.54 | ± 5.45 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 741.18K | ± 30.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 723.99K | ± 25.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 674.46K | ± 9.46K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 673.43K | ± 11.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      63661.561   ± 2732.519  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2090.832    ± 313.089  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1987.327    ± 235.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1972.242    ± 219.626  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57152.908   ± 3172.296  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65807.623    ± 401.623  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63817.147    ± 829.318  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9966.535    ± 299.077  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10295.297    ± 331.417  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10054.772     ± 95.913  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        866.239     ± 31.599  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        688.538      ± 5.454  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7407.910    ± 140.593  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5469.171     ± 77.328  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6999.428    ± 271.076  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     674461.630   ± 9456.572  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     673434.690  ± 11124.469  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     723993.000  ± 25271.951  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     741179.630  ± 30112.662  ops/s
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
