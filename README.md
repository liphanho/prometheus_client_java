# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-03T10:21:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.15K | ± 1.62K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.23K | ± 1.12K | ops/s | 1.2x slower |
| prometheusAdd | 51.39K | ± 128.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.14K | ± 1.68K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 30.33 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 26.19 | ops/s | 10x slower |
| simpleclientAdd | 5.90K | ± 132.04 | ops/s | 11x slower |
| openTelemetryAdd | 1.65K | ± 47.17 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.32K | ± 145.33 | ops/s | 49x slower |
| openTelemetryInc | 1.31K | ± 144.61 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 93.50 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 28.04 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 140.93 | ops/s | 1.8x slower |
| openTelemetryClassic | 723.11 | ± 61.50 | ops/s | 7.4x slower |
| openTelemetryExponential | 551.41 | ± 27.67 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.92K | ± 2.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.41K | ± 3.64K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.02K | ± 6.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.67K | ± 2.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49144.614   ± 1679.953  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1648.316     ± 47.170  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1314.886    ± 144.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.780    ± 145.334  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51389.273    ± 128.419  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65152.465   ± 1623.146  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56226.694   ± 1121.448  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5897.984    ± 132.040  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6572.243     ± 30.332  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6491.309     ± 26.190  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        723.113     ± 61.505  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.410     ± 27.669  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5339.683     ± 93.498  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2970.258    ± 140.927  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4373.077     ± 28.040  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465669.057   ± 2930.277  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470023.409   ± 6297.699  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479408.563   ± 3642.582  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481921.396   ± 2297.697  ops/s
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
