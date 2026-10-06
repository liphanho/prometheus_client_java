# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-06T09:55:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.02K | ± 15.12K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.97K | ± 89.99 | ops/s | 1.0x slower |
| prometheusAdd | 50.81K | ± 527.82 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.13K | ± 126.85 | ops/s | 1.1x slower |
| simpleclientInc | 6.60K | ± 33.57 | ops/s | 8.5x slower |
| simpleclientNoLabelsInc | 6.33K | ± 69.10 | ops/s | 8.9x slower |
| simpleclientAdd | 6.15K | ± 254.56 | ops/s | 9.1x slower |
| openTelemetryAdd | 1.56K | ± 268.73 | ops/s | 36x slower |
| openTelemetryIncNoLabels | 1.35K | ± 223.13 | ops/s | 42x slower |
| openTelemetryInc | 1.31K | ± 46.68 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.98K | ± 156.87 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 24.58 | ops/s | 1.1x slower |
| prometheusNative | 3.17K | ± 198.83 | ops/s | 1.6x slower |
| openTelemetryClassic | 684.12 | ± 44.31 | ops/s | 7.3x slower |
| openTelemetryExponential | 545.47 | ± 1.53 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.20K | ± 5.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.25K | ± 4.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.38K | ± 6.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 498.41K | ± 5.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49125.296    ± 126.853  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1562.223    ± 268.734  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1310.352     ± 46.682  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1349.893    ± 223.131  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50810.617    ± 527.824  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56020.857  ± 15124.982  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54965.367     ± 89.993  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6145.500    ± 254.558  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6600.400     ± 33.573  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6329.237     ± 69.096  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.124     ± 44.314  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.467      ± 1.526  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4984.769    ± 156.872  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3174.277    ± 198.826  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.854     ± 24.578  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507381.112   ± 6526.911  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     498409.316   ± 5787.264  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523245.263   ± 4420.006  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530200.833   ± 5776.429  ops/s
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
