# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-24T13:20:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.45K | ± 73.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.56K | ± 1.11K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.75K | ± 1.31K | ops/s | 1.1x slower |
| prometheusAdd | 28.36K | ± 53.41 | ops/s | 1.1x slower |
| simpleclientInc | 6.48K | ± 176.14 | ops/s | 4.9x slower |
| simpleclientAdd | 6.29K | ± 121.87 | ops/s | 5.0x slower |
| simpleclientNoLabelsInc | 6.23K | ± 348.99 | ops/s | 5.1x slower |
| openTelemetryInc | 1.33K | ± 33.50 | ops/s | 24x slower |
| openTelemetryIncNoLabels | 1.29K | ± 91.87 | ops/s | 24x slower |
| openTelemetryAdd | 1.18K | ± 12.30 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.21K | ± 119.45 | ops/s | **fastest** |
| prometheusClassic | 3.09K | ± 207.19 | ops/s | 1.4x slower |
| prometheusNative | 2.18K | ± 124.97 | ops/s | 1.9x slower |
| openTelemetryClassic | 520.96 | ± 42.60 | ops/s | 8.1x slower |
| openTelemetryExponential | 432.70 | ± 16.44 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 334.49K | ± 2.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 333.15K | ± 2.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.08K | ± 1.96K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 307.56K | ± 1.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28746.568   ± 1305.197  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1180.035     ± 12.300  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1325.426     ± 33.496  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1288.563     ± 91.869  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28357.378     ± 53.409  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31452.584     ± 73.755  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30559.374   ± 1108.954  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6287.876    ± 121.870  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6483.558    ± 176.137  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6225.270    ± 348.992  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        520.962     ± 42.603  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        432.702     ± 16.445  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3085.585    ± 207.191  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2175.912    ± 124.965  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4207.049    ± 119.447  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     307563.281   ± 1376.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     312080.297   ± 1960.208  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     333154.517   ± 2403.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     334485.770   ± 2523.463  ops/s
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
