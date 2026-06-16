# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-16T08:44:32Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.43K | ± 181.66 | ops/s | **fastest** |
| prometheusInc | 30.66K | ± 1.22K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.06K | ± 1.00K | ops/s | 1.1x slower |
| prometheusAdd | 28.30K | ± 402.10 | ops/s | 1.1x slower |
| simpleclientInc | 6.85K | ± 136.50 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.77K | ± 212.39 | ops/s | 4.6x slower |
| simpleclientAdd | 6.58K | ± 198.54 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.43K | ± 138.35 | ops/s | 22x slower |
| openTelemetryInc | 1.42K | ± 35.41 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.37K | ± 114.07 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 109.89 | ops/s | **fastest** |
| prometheusClassic | 2.95K | ± 114.78 | ops/s | 1.5x slower |
| prometheusNative | 2.07K | ± 152.01 | ops/s | 2.1x slower |
| openTelemetryClassic | 541.02 | ± 23.42 | ops/s | 8.2x slower |
| openTelemetryExponential | 411.09 | ± 8.95 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 341.88K | ± 1.41K | ops/s | **fastest** |
| prometheusWriteToByteArray | 336.94K | ± 2.76K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 311.35K | ± 1.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 309.45K | ± 2.49K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29057.015   ± 1004.597  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.907    ± 138.349  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.128     ± 35.410  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1367.819    ± 114.067  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28298.966    ± 402.099  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30657.009   ± 1220.736  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31428.051    ± 181.661  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6580.923    ± 198.541  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6853.379    ± 136.500  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6767.964    ± 212.394  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        541.016     ± 23.421  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        411.090      ± 8.947  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2948.784    ± 114.784  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2074.225    ± 152.013  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.129    ± 109.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     309450.784   ± 2488.892  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     311347.731   ± 1783.773  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     336938.631   ± 2755.615  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     341883.799   ± 1412.016  ops/s
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
