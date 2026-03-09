# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-09T05:36:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.62K | ± 15.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.29K | ± 1.37K | ops/s | 1.0x slower |
| prometheusAdd | 51.74K | ± 176.14 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 47.09K | ± 990.26 | ops/s | 1.2x slower |
| simpleclientInc | 6.77K | ± 33.16 | ops/s | 8.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 123.00 | ops/s | 8.6x slower |
| simpleclientAdd | 6.44K | ± 139.62 | ops/s | 8.8x slower |
| openTelemetryAdd | 1.57K | ± 212.54 | ops/s | 36x slower |
| openTelemetryInc | 1.26K | ± 27.18 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.21K | ± 28.37 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 87.78 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 28.29 | ops/s | 1.2x slower |
| prometheusNative | 3.11K | ± 36.26 | ops/s | 1.7x slower |
| openTelemetryClassic | 727.82 | ± 46.47 | ops/s | 7.3x slower |
| openTelemetryExponential | 533.88 | ± 17.36 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.64K | ± 7.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.63K | ± 5.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.69K | ± 6.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.62K | ± 6.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47087.633    ± 990.261  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1566.824    ± 212.540  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.023     ± 27.175  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.398     ± 28.371  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51741.799    ± 176.141  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56622.070  ± 15530.084  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56293.309   ± 1372.054  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6440.413    ± 139.618  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6769.527     ± 33.162  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6595.481    ± 122.996  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        727.816     ± 46.467  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.876     ± 17.356  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5288.692     ± 87.781  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3112.906     ± 36.256  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4540.854     ± 28.288  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515691.315   ± 6493.983  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510616.177   ± 6660.738  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528630.850   ± 5373.905  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532643.769   ± 7169.666  ops/s
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
