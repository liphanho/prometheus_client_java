# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-11T05:39:20Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.40K | ± 148.82 | ops/s | **fastest** |
| prometheusInc | 30.97K | ± 856.27 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.18K | ± 165.70 | ops/s | 1.1x slower |
| prometheusAdd | 28.43K | ± 351.81 | ops/s | 1.1x slower |
| simpleclientInc | 6.80K | ± 113.30 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.68K | ± 106.20 | ops/s | 4.7x slower |
| simpleclientAdd | 6.40K | ± 188.88 | ops/s | 4.9x slower |
| openTelemetryInc | 1.46K | ± 36.37 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 1.43K | ± 100.02 | ops/s | 22x slower |
| openTelemetryAdd | 1.27K | ± 30.83 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 23.94 | ops/s | **fastest** |
| prometheusClassic | 2.89K | ± 209.40 | ops/s | 1.5x slower |
| prometheusNative | 2.08K | ± 209.96 | ops/s | 2.2x slower |
| openTelemetryClassic | 498.38 | ± 21.17 | ops/s | 9.0x slower |
| openTelemetryExponential | 388.83 | ± 15.75 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 323.21K | ± 2.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 321.22K | ± 4.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.03K | ± 1.87K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.04K | ± 1.78K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29182.726    ± 165.696  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1273.063     ± 30.826  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1463.346     ± 36.369  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1429.933    ± 100.019  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28425.152    ± 351.806  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30965.651    ± 856.267  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31404.203    ± 148.822  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6403.342    ± 188.883  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6798.652    ± 113.300  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6679.328    ± 106.198  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        498.384     ± 21.174  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        388.833     ± 15.753  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2892.543    ± 209.401  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2076.395    ± 209.960  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4478.724     ± 23.942  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294037.626   ± 1781.274  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298033.743   ± 1866.364  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     321216.558   ± 4697.315  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     323212.210   ± 2680.454  ops/s
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
