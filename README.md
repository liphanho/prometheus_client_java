# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-08T09:46:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.97K | ± 459.85 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 494.62 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 67.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.18K | ± 764.62 | ops/s | 1.4x slower |
| simpleclientInc | 6.62K | ± 102.88 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 142.58 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 182.66 | ops/s | 11x slower |
| openTelemetryAdd | 1.54K | ± 242.63 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.35K | ± 147.47 | ops/s | 50x slower |
| openTelemetryInc | 1.32K | ± 34.29 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 413.86 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 40.21 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 191.80 | ops/s | 1.7x slower |
| openTelemetryClassic | 693.81 | ± 13.65 | ops/s | 7.7x slower |
| openTelemetryExponential | 543.98 | ± 18.16 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 527.93K | ± 6.26K | ops/s | **fastest** |
| prometheusWriteToNull | 527.67K | ± 10.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.78K | ± 4.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 502.54K | ± 2.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48176.511    ± 764.619  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1535.730    ± 242.632  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1321.158     ± 34.293  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1345.146    ± 147.471  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51351.322     ± 67.245  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66973.444    ± 459.848  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56730.806    ± 494.617  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6210.953    ± 182.665  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6623.487    ± 102.883  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6437.078    ± 142.576  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.815     ± 13.646  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.981     ± 18.162  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5310.994    ± 413.856  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3165.714    ± 191.804  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.265     ± 40.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505776.658   ± 4921.979  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     502544.915   ± 2935.439  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527930.874   ± 6259.481  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527671.086  ± 10641.011  ops/s
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
