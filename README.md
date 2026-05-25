# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-25T07:52:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.08K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.96K | ± 1.20K | ops/s | 1.2x slower |
| prometheusAdd | 51.44K | ± 203.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.61K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 202.51 | ops/s | 9.9x slower |
| simpleclientAdd | 6.48K | ± 19.93 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 194.02 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 190.12 | ops/s | 42x slower |
| openTelemetryInc | 1.41K | ± 193.92 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.31K | ± 136.39 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 52.82 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 57.25 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 154.75 | ops/s | 1.8x slower |
| openTelemetryClassic | 683.84 | ± 34.97 | ops/s | 7.8x slower |
| openTelemetryExponential | 566.29 | ± 18.16 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.10K | ± 2.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.48K | ± 5.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.09K | ± 5.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.51K | ± 1.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49613.249   ± 1284.498  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1561.751    ± 190.124  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1406.703    ± 193.921  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1311.121    ± 136.390  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51439.734    ± 203.389  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65081.047   ± 1280.709  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55958.100   ± 1197.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6481.900     ± 19.932  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6601.501    ± 202.505  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6403.745    ± 194.017  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.836     ± 34.974  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.289     ± 18.165  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5304.208     ± 52.816  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2966.544    ± 154.748  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.848     ± 57.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507505.643   ± 1732.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514086.823   ± 5580.884  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529478.218   ± 5868.251  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534104.386   ± 2167.695  ops/s
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
