# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T06:38:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.43K | ± 74.84 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.14K | ± 2.07K | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 206.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.15K | ± 1.59K | ops/s | 1.4x slower |
| simpleclientInc | 6.46K | ± 198.72 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 232.35 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 257.18 | ops/s | 11x slower |
| openTelemetryAdd | 1.25K | ± 44.04 | ops/s | 53x slower |
| openTelemetryInc | 1.20K | ± 36.43 | ops/s | 55x slower |
| openTelemetryIncNoLabels | 1.20K | ± 23.86 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 82.39 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 53.24 | ops/s | 1.2x slower |
| prometheusNative | 3.11K | ± 35.27 | ops/s | 1.7x slower |
| openTelemetryClassic | 670.54 | ± 40.63 | ops/s | 7.7x slower |
| openTelemetryExponential | 540.21 | ± 14.27 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 523.65K | ± 2.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.99K | ± 5.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 496.82K | ± 1.47K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 492.57K | ± 2.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48152.677   ± 1591.226  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.932     ± 44.042  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1202.911     ± 36.426  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1198.599     ± 23.858  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51595.164    ± 206.026  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66433.227     ± 74.842  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55141.324   ± 2065.229  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6157.601    ± 257.181  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6455.885    ± 198.722  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.149    ± 232.349  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        670.538     ± 40.627  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.211     ± 14.274  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5157.502     ± 82.395  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3111.526     ± 35.275  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4482.039     ± 53.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     496818.796   ± 1470.986  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492566.874   ± 2056.020  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505990.527   ± 5254.501  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     523654.243   ± 2490.973  ops/s
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
