# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-09T05:51:31Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.67K | ± 722.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.87K | ± 276.79 | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 98.75 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.10K | ± 1.73K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 22.17 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.53K | ± 130.19 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 264.03 | ops/s | 11x slower |
| openTelemetryAdd | 1.38K | ± 195.90 | ops/s | 47x slower |
| openTelemetryInc | 1.32K | ± 104.58 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.32K | ± 192.52 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 277.82 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 56.59 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 131.62 | ops/s | 1.8x slower |
| openTelemetryClassic | 747.93 | ± 38.19 | ops/s | 7.1x slower |
| openTelemetryExponential | 585.31 | ± 32.63 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.31K | ± 4.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 535.62K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.91K | ± 7.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.98K | ± 2.59K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49097.972   ± 1726.084  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1382.583    ± 195.899  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1321.425    ± 104.579  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1320.449    ± 192.517  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51578.990     ± 98.751  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65666.005    ± 722.564  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56870.940    ± 276.791  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6146.046    ± 264.028  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.113     ± 22.173  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6527.145    ± 130.187  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        747.928     ± 38.187  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.310     ± 32.632  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5345.097    ± 277.825  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2904.297    ± 131.616  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.619     ± 56.589  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521905.939   ± 7501.649  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519984.751   ± 2591.196  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     535623.054   ± 2122.202  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540313.171   ± 4569.196  ops/s
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
