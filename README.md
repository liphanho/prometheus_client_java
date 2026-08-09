# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T04:59:28Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.55K | ± 931.74 | ops/s | **fastest** |
| prometheusAdd | 51.15K | ± 358.86 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 49.26K | ± 9.67K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.32K | ± 1.43K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 183.61 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.51K | ± 124.13 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 268.01 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 188.21 | ops/s | 42x slower |
| openTelemetryInc | 1.37K | ± 174.61 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.16K | ± 44.95 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 7.06 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 56.06 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 146.61 | ops/s | 1.8x slower |
| openTelemetryClassic | 665.48 | ± 11.17 | ops/s | 7.9x slower |
| openTelemetryExponential | 560.77 | ± 15.74 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 517.77K | ± 8.37K | ops/s | **fastest** |
| prometheusWriteToNull | 506.62K | ± 13.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.14K | ± 2.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 493.88K | ± 5.87K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48317.140   ± 1429.293  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1561.442    ± 188.211  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.180    ± 174.607  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1160.127     ± 44.945  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51153.460    ± 358.862  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65546.739    ± 931.741  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49261.176   ± 9673.773  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6310.997    ± 268.006  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.280    ± 183.607  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6513.293    ± 124.131  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.485     ± 11.171  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.774     ± 15.741  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5229.218      ± 7.055  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2945.347    ± 146.614  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4423.098     ± 56.058  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499136.249   ± 2967.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     493881.348   ± 5874.867  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517766.675   ± 8370.934  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506616.389  ± 13933.398  ops/s
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
