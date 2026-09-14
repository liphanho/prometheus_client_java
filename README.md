# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-14T08:54:17Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.27K | ± 227.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.18K | ± 1.37K | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 329.80 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.92K | ± 1.17K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 26.46 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.42K | ± 125.94 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 93.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.62K | ± 235.65 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.48K | ± 39.44 | ops/s | 45x slower |
| openTelemetryInc | 1.41K | ± 172.64 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 242.44 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 9.97 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 52.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 705.01 | ± 34.49 | ops/s | 7.4x slower |
| openTelemetryExponential | 558.18 | ± 11.12 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.63K | ± 7.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.14K | ± 3.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.49K | ± 5.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.23K | ± 4.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48916.589   ± 1174.856  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1622.067    ± 235.649  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.182    ± 172.640  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1475.005     ± 39.445  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51491.430    ± 329.799  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66266.921    ± 227.592  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56181.744   ± 1368.287  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6030.931     ± 93.849  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6685.705     ± 26.457  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6423.361    ± 125.944  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.012     ± 34.487  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.177     ± 11.123  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5222.510    ± 242.440  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3147.154     ± 52.645  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4388.798      ± 9.970  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505225.166   ± 4854.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506490.624   ± 5246.209  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521144.691   ± 3113.003  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529625.274   ± 7241.343  ops/s
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
