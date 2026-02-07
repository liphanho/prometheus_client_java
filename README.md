# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-07T05:25:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.35K | ± 1.50K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 342.12 | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 265.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.95K | ± 1.69K | ops/s | 1.3x slower |
| simpleclientInc | 6.78K | ± 35.63 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.70K | ± 9.56 | ops/s | 9.9x slower |
| simpleclientAdd | 6.17K | ± 326.45 | ops/s | 11x slower |
| openTelemetryInc | 1.35K | ± 111.51 | ops/s | 49x slower |
| openTelemetryAdd | 1.35K | ± 191.89 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.18K | ± 40.01 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 316.85 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 18.54 | ops/s | 1.1x slower |
| prometheusNative | 3.02K | ± 47.43 | ops/s | 1.7x slower |
| openTelemetryClassic | 645.76 | ± 6.11 | ops/s | 7.8x slower |
| openTelemetryExponential | 548.12 | ± 15.86 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 515.50K | ± 5.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 511.90K | ± 2.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 501.60K | ± 6.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.69K | ± 3.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49951.319   ± 1688.919  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1346.822    ± 191.891  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.404    ± 111.507  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1183.921     ± 40.012  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51642.114    ± 265.309  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66349.978   ± 1497.190  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56795.951    ± 342.120  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6169.627    ± 326.446  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6781.001     ± 35.626  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6699.850      ± 9.564  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        645.756      ± 6.108  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.119     ± 15.857  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5057.875    ± 316.850  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.008     ± 47.429  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.776     ± 18.544  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495691.305   ± 3850.815  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     501595.201   ± 6358.870  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     511897.462   ± 2087.196  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515500.145   ± 5973.533  ops/s
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
