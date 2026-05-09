# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-09T06:39:01Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.50K | ± 2.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.43K | ± 398.23 | ops/s | 1.1x slower |
| prometheusAdd | 48.21K | ± 554.02 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.09K | ± 251.87 | ops/s | 1.3x slower |
| simpleclientInc | 6.29K | ± 42.28 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.11K | ± 117.47 | ops/s | 9.6x slower |
| simpleclientAdd | 5.93K | ± 214.66 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.36K | ± 61.76 | ops/s | 43x slower |
| openTelemetryAdd | 1.35K | ± 17.12 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 76.58 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.02K | ± 421.88 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 72.54 | ops/s | 1.1x slower |
| prometheusNative | 3.09K | ± 54.61 | ops/s | 1.6x slower |
| openTelemetryClassic | 618.56 | ± 20.26 | ops/s | 8.1x slower |
| openTelemetryExponential | 505.38 | ± 24.23 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 634.29K | ± 7.88K | ops/s | **fastest** |
| prometheusWriteToByteArray | 627.04K | ± 6.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 604.30K | ± 11.59K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 600.79K | ± 5.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44094.439    ± 251.874  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1352.480     ± 17.121  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.646     ± 76.578  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1355.558     ± 61.759  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48214.186    ± 554.021  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58503.681   ± 2077.009  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51434.047    ± 398.234  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5929.300    ± 214.664  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6289.797     ± 42.283  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6112.932    ± 117.471  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        618.565     ± 20.264  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        505.384     ± 24.228  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5019.043    ± 421.885  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3086.642     ± 54.610  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4502.208     ± 72.541  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     600786.546   ± 5604.997  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     604304.553  ± 11587.161  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     627036.995   ± 6676.045  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     634292.557   ± 7877.551  ops/s
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
