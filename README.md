# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T08:00:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.90K | ± 320.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.91K | ± 597.93 | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 347.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.42K | ± 1.41K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 12.34 | ops/s | 10.0x slower |
| simpleclientInc | 6.57K | ± 199.37 | ops/s | 10x slower |
| simpleclientAdd | 6.47K | ± 22.78 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 156.35 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.35K | ± 225.34 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 53.95 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 186.84 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 64.39 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 160.21 | ops/s | 1.8x slower |
| openTelemetryClassic | 700.82 | ± 14.05 | ops/s | 7.7x slower |
| openTelemetryExponential | 583.68 | ± 39.86 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.73K | ± 4.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.85K | ± 3.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.59K | ± 10.51K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 502.86K | ± 3.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48422.036   ± 1408.790  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.225     ± 53.953  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1396.470    ± 156.352  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1346.129    ± 225.344  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51221.376    ± 347.460  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65895.932    ± 320.231  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55911.819    ± 597.934  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6466.890     ± 22.781  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6565.465    ± 199.374  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6613.847     ± 12.336  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.820     ± 14.048  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.682     ± 39.865  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5416.003    ± 186.843  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2949.602    ± 160.205  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4446.048     ± 64.385  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     502862.199   ± 3217.889  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506589.352  ± 10507.515  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529849.173   ± 3795.980  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532728.149   ± 4577.558  ops/s
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
