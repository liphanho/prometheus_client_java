# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-10T10:38:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.14K | ± 3.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.31K | ± 391.24 | ops/s | 1.2x slower |
| prometheusAdd | 61.56K | ± 732.92 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.76K | ± 1.81K | ops/s | 1.3x slower |
| simpleclientInc | 7.99K | ± 29.43 | ops/s | 9.4x slower |
| simpleclientAdd | 7.62K | ± 292.87 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.50K | ± 424.86 | ops/s | 10x slower |
| openTelemetryInc | 1.88K | ± 234.84 | ops/s | 40x slower |
| openTelemetryAdd | 1.82K | ± 122.58 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.70K | ± 22.34 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.25K | ± 121.60 | ops/s | **fastest** |
| simpleclient | 5.77K | ± 93.99 | ops/s | 1.3x slower |
| prometheusNative | 3.88K | ± 108.79 | ops/s | 1.9x slower |
| openTelemetryClassic | 810.91 | ± 51.76 | ops/s | 8.9x slower |
| openTelemetryExponential | 701.18 | ± 28.30 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 746.66K | ± 10.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 738.90K | ± 4.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 690.89K | ± 4.65K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 679.46K | ± 4.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55763.178   ± 1808.736  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1815.799    ± 122.584  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1884.326    ± 234.840  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1704.790     ± 22.340  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61555.421    ± 732.922  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75141.233   ± 3139.794  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65310.588    ± 391.243  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7620.944    ± 292.866  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7991.378     ± 29.433  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7497.176    ± 424.861  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        810.908     ± 51.759  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        701.182     ± 28.297  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7247.218    ± 121.597  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3881.984    ± 108.789  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5773.487     ± 93.995  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     679458.563   ± 4529.705  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     690889.543   ± 4646.566  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     738897.277   ± 4667.314  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     746659.289  ± 10594.799  ops/s
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
