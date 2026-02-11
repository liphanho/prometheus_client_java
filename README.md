# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-11T05:46:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 660.17 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 534.16 | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 167.63 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.39K | ± 809.48 | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 16.38 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.56K | ± 203.58 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 223.71 | ops/s | 10x slower |
| openTelemetryInc | 1.45K | ± 183.38 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.40K | ± 107.40 | ops/s | 47x slower |
| openTelemetryAdd | 1.37K | ± 150.88 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.33K | ± 272.69 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 24.55 | ops/s | 1.2x slower |
| prometheusNative | 3.11K | ± 55.00 | ops/s | 1.7x slower |
| openTelemetryClassic | 670.00 | ± 2.04 | ops/s | 8.0x slower |
| openTelemetryExponential | 536.87 | ± 21.60 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.18K | ± 2.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.82K | ± 13.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 524.63K | ± 4.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.95K | ± 7.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48394.961    ± 809.484  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1373.863    ± 150.884  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1451.486    ± 183.377  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1396.079    ± 107.402  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51639.265    ± 167.628  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66035.791    ± 660.168  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56730.640    ± 534.162  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6292.531    ± 223.705  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6757.985     ± 16.377  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6563.554    ± 203.579  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        669.998      ± 2.042  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.867     ± 21.596  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5334.760    ± 272.692  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3111.417     ± 55.004  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.713     ± 24.551  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514945.758   ± 7228.804  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524626.728   ± 4606.095  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533817.790  ± 13786.788  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537183.288   ± 2638.620  ops/s
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
