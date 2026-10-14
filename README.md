# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-14T08:27:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 30.87K | ± 227.67 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.83K | ± 1.56K | ops/s | 1.0x slower |
| prometheusInc | 29.69K | ± 402.31 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 29.61K | ± 912.52 | ops/s | 1.0x slower |
| simpleclientInc | 7.70K | ± 154.02 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.53K | ± 113.17 | ops/s | 4.1x slower |
| simpleclientAdd | 7.47K | ± 236.84 | ops/s | 4.1x slower |
| openTelemetryAdd | 910.62 | ± 61.62 | ops/s | 34x slower |
| openTelemetryIncNoLabels | 907.73 | ± 25.53 | ops/s | 34x slower |
| openTelemetryInc | 827.36 | ± 36.26 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.09K | ± 23.25 | ops/s | **fastest** |
| prometheusClassic | 2.43K | ± 147.51 | ops/s | 2.1x slower |
| prometheusNative | 1.80K | ± 39.04 | ops/s | 2.8x slower |
| openTelemetryClassic | 373.62 | ± 11.18 | ops/s | 14x slower |
| openTelemetryExponential | 330.67 | ± 41.85 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.27K | ± 5.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 311.96K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 293.58K | ± 1.46K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 291.29K | ± 1.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30827.706   ± 1559.548  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        910.620     ± 61.617  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        827.362     ± 36.261  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        907.729     ± 25.531  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      30871.483    ± 227.665  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29688.280    ± 402.310  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29609.207    ± 912.515  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7466.948    ± 236.838  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7701.843    ± 154.022  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7533.988    ± 113.173  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        373.625     ± 11.181  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        330.669     ± 41.854  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2427.743    ± 147.510  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1796.277     ± 39.037  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5090.814     ± 23.254  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293579.915   ± 1456.261  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     291287.640   ± 1864.740  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     311957.737   ± 3306.691  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317267.270   ± 5426.537  ops/s
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
