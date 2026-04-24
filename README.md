# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-24T06:11:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.92K | ± 230.29 | ops/s | **fastest** |
| prometheusInc | 30.74K | ± 1.23K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.14K | ± 986.34 | ops/s | 1.0x slower |
| prometheusAdd | 28.31K | ± 273.78 | ops/s | 1.1x slower |
| simpleclientInc | 6.99K | ± 67.77 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.91K | ± 91.08 | ops/s | 4.5x slower |
| simpleclientAdd | 6.65K | ± 110.10 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.47K | ± 65.97 | ops/s | 21x slower |
| openTelemetryInc | 1.46K | ± 32.51 | ops/s | 21x slower |
| openTelemetryAdd | 1.39K | ± 47.38 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.55K | ± 108.08 | ops/s | **fastest** |
| prometheusClassic | 3.03K | ± 180.29 | ops/s | 1.5x slower |
| prometheusNative | 2.31K | ± 196.66 | ops/s | 2.0x slower |
| openTelemetryClassic | 528.91 | ± 14.93 | ops/s | 8.6x slower |
| openTelemetryExponential | 409.63 | ± 10.29 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 336.24K | ± 2.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 330.65K | ± 3.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 305.34K | ± 1.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 301.44K | ± 3.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30144.610    ± 986.342  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1392.019     ± 47.379  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1455.851     ± 32.506  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1471.701     ± 65.972  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28309.989    ± 273.777  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30737.300   ± 1231.928  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30917.453    ± 230.286  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6646.240    ± 110.103  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6994.700     ± 67.770  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6905.587     ± 91.082  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        528.915     ± 14.930  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        409.626     ± 10.293  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3032.326    ± 180.291  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2311.178    ± 196.660  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4551.106    ± 108.078  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     301444.957   ± 3533.687  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     305335.265   ± 1435.444  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     330649.443   ± 3576.117  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     336241.201   ± 2784.149  ops/s
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
