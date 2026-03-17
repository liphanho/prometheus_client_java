# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-17T05:37:09Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.03K | ± 5.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 343.28 | ops/s | 1.1x slower |
| prometheusAdd | 51.24K | ± 776.15 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.95K | ± 1.66K | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 20.03 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.56K | ± 217.69 | ops/s | 9.6x slower |
| simpleclientAdd | 6.39K | ± 248.21 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.50K | ± 242.79 | ops/s | 42x slower |
| openTelemetryInc | 1.41K | ± 188.16 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.21K | ± 57.48 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 37.59 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 19.00 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 14.66 | ops/s | 1.7x slower |
| openTelemetryClassic | 685.68 | ± 15.82 | ops/s | 7.8x slower |
| openTelemetryExponential | 545.59 | ± 21.15 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.17K | ± 3.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.01K | ± 5.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.43K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.01K | ± 4.62K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47950.251   ± 1663.164  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1503.187    ± 242.792  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1412.442    ± 188.157  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1206.777     ± 57.476  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51236.264    ± 776.148  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63027.631   ± 5137.591  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56797.045    ± 343.275  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6393.450    ± 248.210  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6767.513     ± 20.033  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6560.062    ± 217.690  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.680     ± 15.824  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.585     ± 21.147  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5350.754     ± 37.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3115.214     ± 14.659  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4535.852     ± 19.003  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515430.187   ± 4108.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514009.339   ± 4620.358  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526006.563   ± 5310.539  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541173.706   ± 3017.638  ops/s
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
