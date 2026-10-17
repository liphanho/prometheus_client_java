# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-17T07:55:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 1.03K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 436.05 | ops/s | 1.2x slower |
| prometheusAdd | 50.91K | ± 588.26 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.19K | ± 1.58K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 180.33 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.40K | ± 172.37 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 230.42 | ops/s | 10x slower |
| openTelemetryInc | 1.51K | ± 189.89 | ops/s | 44x slower |
| openTelemetryAdd | 1.34K | ± 157.10 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.19K | ± 41.25 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 191.45 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 22.55 | ops/s | 1.2x slower |
| prometheusNative | 2.89K | ± 154.89 | ops/s | 1.8x slower |
| openTelemetryClassic | 679.18 | ± 6.77 | ops/s | 7.7x slower |
| openTelemetryExponential | 591.44 | ± 41.02 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.74K | ± 9.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.78K | ± 12.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.67K | ± 12.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.38K | ± 7.53K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49186.086   ± 1577.378  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1342.840    ± 157.096  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1508.263    ± 189.892  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1188.629     ± 41.246  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50912.388    ± 588.258  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65824.659   ± 1034.657  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56590.686    ± 436.051  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6322.253    ± 230.419  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6585.554    ± 180.332  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6399.997    ± 172.373  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.179      ± 6.767  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        591.445     ± 41.024  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5218.298    ± 191.451  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2892.233    ± 154.889  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4368.484     ± 22.549  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486673.908  ± 12815.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482381.143   ± 7527.700  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493781.494  ± 12840.437  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499736.683   ± 9829.822  ops/s
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
