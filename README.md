# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-24T05:37:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.21K | ± 1.49K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 317.82 | ops/s | 1.1x slower |
| prometheusAdd | 51.42K | ± 349.19 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.98K | ± 1.43K | ops/s | 1.3x slower |
| simpleclientInc | 6.81K | ± 10.32 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.41K | ± 86.00 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 214.92 | ops/s | 10x slower |
| openTelemetryAdd | 1.63K | ± 55.43 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.29K | ± 119.24 | ops/s | 50x slower |
| openTelemetryInc | 1.28K | ± 36.90 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 150.43 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 30.73 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 141.62 | ops/s | 1.8x slower |
| openTelemetryClassic | 668.33 | ± 30.37 | ops/s | 8.1x slower |
| openTelemetryExponential | 527.13 | ± 15.61 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.89K | ± 4.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.03K | ± 4.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.76K | ± 8.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.33K | ± 2.47K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48981.518   ± 1428.125  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1626.371     ± 55.427  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1276.120     ± 36.898  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1292.690    ± 119.239  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51419.957    ± 349.185  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65211.467   ± 1488.029  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57002.224    ± 317.818  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6297.269    ± 214.917  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6805.858     ± 10.318  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6406.890     ± 85.998  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.333     ± 30.370  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.126     ± 15.606  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5409.553    ± 150.433  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3056.605    ± 141.621  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4510.823     ± 30.727  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510330.942   ± 2467.132  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522758.228   ± 8597.994  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523029.648   ± 4104.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529892.298   ± 4950.959  ops/s
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
