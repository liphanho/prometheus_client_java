# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-08T06:38:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.01K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 333.56 | ops/s | 1.1x slower |
| prometheusAdd | 50.78K | ± 448.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.63K | ± 705.54 | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 60.95 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.56K | ± 93.92 | ops/s | 9.9x slower |
| simpleclientAdd | 5.97K | ± 27.43 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 276.73 | ops/s | 45x slower |
| openTelemetryInc | 1.32K | ± 131.69 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.31K | ± 228.43 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 213.42 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 22.31 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 90.47 | ops/s | 1.7x slower |
| openTelemetryClassic | 679.19 | ± 17.67 | ops/s | 7.6x slower |
| openTelemetryExponential | 559.49 | ± 25.28 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.71K | ± 6.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.24K | ± 12.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.89K | ± 4.33K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 505.42K | ± 13.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50630.304    ± 705.540  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1450.536    ± 276.725  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.951    ± 131.686  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.498    ± 228.435  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50775.684    ± 448.774  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65014.271   ± 1209.716  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56711.092    ± 333.560  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5973.046     ± 27.428  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6665.565     ± 60.952  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6556.103     ± 93.915  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.188     ± 17.668  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.486     ± 25.281  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5138.071    ± 213.422  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.490     ± 90.470  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.990     ± 22.312  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505893.356   ± 4329.091  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505423.377  ± 13547.748  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523243.816  ± 12375.320  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534714.586   ± 6454.985  ops/s
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
