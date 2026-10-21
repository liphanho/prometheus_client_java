# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-21T08:25:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 309.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 469.87 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 201.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.15K | ± 1.58K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 183.45 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.41K | ± 166.76 | ops/s | 10x slower |
| simpleclientAdd | 6.02K | ± 51.61 | ops/s | 11x slower |
| openTelemetryInc | 1.58K | ± 82.35 | ops/s | 42x slower |
| openTelemetryAdd | 1.45K | ± 256.33 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.38K | ± 125.52 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 30.38 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 50.53 | ops/s | 1.3x slower |
| prometheusNative | 3.13K | ± 71.77 | ops/s | 1.8x slower |
| openTelemetryClassic | 725.85 | ± 22.05 | ops/s | 7.6x slower |
| openTelemetryExponential | 575.41 | ± 32.68 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 513.89K | ± 11.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 509.76K | ± 10.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 494.32K | ± 4.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.20K | ± 5.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49152.885   ± 1577.419  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1448.026    ± 256.329  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1579.258     ± 82.347  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1384.590    ± 125.518  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51350.414    ± 201.429  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66180.619    ± 309.207  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56847.365    ± 469.872  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6019.754     ± 51.611  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6583.575    ± 183.454  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6412.588    ± 166.765  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        725.845     ± 22.051  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.407     ± 32.684  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5503.924     ± 30.382  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3130.760     ± 71.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4361.977     ± 50.526  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     494318.223   ± 4382.640  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487199.615   ± 5592.867  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509757.596  ± 10017.047  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513890.459  ± 11714.269  ops/s
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
