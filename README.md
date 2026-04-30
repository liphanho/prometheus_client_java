# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-30T06:47:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.11K | ± 331.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 430.35 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 453.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.27K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 91.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.50K | ± 190.06 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 16.07 | ops/s | 10x slower |
| openTelemetryAdd | 1.30K | ± 19.65 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.28K | ± 150.29 | ops/s | 52x slower |
| openTelemetryInc | 1.23K | ± 64.31 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.68K | ± 139.31 | ops/s | **fastest** |
| simpleclient | 4.32K | ± 53.45 | ops/s | 1.3x slower |
| prometheusNative | 3.12K | ± 134.88 | ops/s | 1.8x slower |
| openTelemetryClassic | 729.60 | ± 25.52 | ops/s | 7.8x slower |
| openTelemetryExponential | 587.10 | ± 30.72 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.34K | ± 4.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 530.55K | ± 4.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.44K | ± 4.03K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 503.67K | ± 11.26K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49271.869   ± 1502.610  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1303.751     ± 19.650  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1234.998     ± 64.306  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1275.216    ± 150.291  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51046.412    ± 453.697  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66110.078    ± 331.352  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56987.839    ± 430.352  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6484.320     ± 16.074  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6645.122     ± 91.584  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6501.148    ± 190.062  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        729.600     ± 25.520  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.098     ± 30.725  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5684.057    ± 139.311  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3116.162    ± 134.878  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4315.454     ± 53.454  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505437.754   ± 4031.847  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     503668.030  ± 11256.984  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530545.208   ± 4016.889  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532341.667   ± 4027.843  ops/s
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
