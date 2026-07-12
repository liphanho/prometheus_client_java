# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T06:45:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.70K | ± 376.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 367.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 34.45 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 205.92 | ops/s | 11x slower |
| simpleclientAdd | 6.17K | ± 252.08 | ops/s | 11x slower |
| openTelemetryAdd | 1.71K | ± 77.85 | ops/s | 39x slower |
| openTelemetryInc | 1.37K | ± 154.91 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 23.98 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.40K | ± 306.98 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 10.48 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 98.82 | ops/s | 1.8x slower |
| openTelemetryClassic | 696.48 | ± 26.40 | ops/s | 7.7x slower |
| openTelemetryExponential | 548.72 | ± 16.56 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 498.92K | ± 31.73K | ops/s | **fastest** |
| prometheusWriteToNull | 492.93K | ± 33.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.53K | ± 28.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.63K | ± 24.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49416.252   ± 1513.196  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1713.147     ± 77.846  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1371.560    ± 154.911  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1206.726     ± 23.980  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51205.302    ± 367.380  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66695.287    ± 376.595  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56445.149   ± 1092.407  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6170.160    ± 252.081  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.988     ± 34.454  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6330.647    ± 205.916  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.483     ± 26.399  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.723     ± 16.564  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5397.560    ± 306.980  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2953.135     ± 98.816  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.426     ± 10.484  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473626.478  ± 24338.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481531.993  ± 28964.618  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498916.929  ± 31729.877  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492930.040  ± 33903.982  ops/s
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
