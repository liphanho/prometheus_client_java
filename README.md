# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-05T05:32:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.61K | ± 37.60 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.86K | ± 1.01K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 29.68K | ± 877.21 | ops/s | 1.1x slower |
| prometheusAdd | 28.63K | ± 152.97 | ops/s | 1.1x slower |
| simpleclientInc | 7.08K | ± 114.52 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.73K | ± 92.90 | ops/s | 4.7x slower |
| simpleclientAdd | 6.69K | ± 93.50 | ops/s | 4.7x slower |
| openTelemetryInc | 1.37K | ± 93.81 | ops/s | 23x slower |
| openTelemetryIncNoLabels | 1.36K | ± 51.33 | ops/s | 23x slower |
| openTelemetryAdd | 1.34K | ± 12.32 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.56K | ± 21.81 | ops/s | **fastest** |
| prometheusClassic | 2.86K | ± 360.75 | ops/s | 1.6x slower |
| prometheusNative | 2.20K | ± 170.83 | ops/s | 2.1x slower |
| openTelemetryClassic | 492.50 | ± 20.80 | ops/s | 9.3x slower |
| openTelemetryExponential | 407.30 | ± 13.30 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 334.44K | ± 2.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 332.92K | ± 3.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 312.21K | ± 993.38 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 309.09K | ± 372.16 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29675.345    ± 877.206  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1342.073     ± 12.315  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1369.295     ± 93.806  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1363.487     ± 51.325  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28627.202    ± 152.973  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31608.286     ± 37.603  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29857.979   ± 1014.270  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6688.535     ± 93.496  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7082.848    ± 114.520  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6729.390     ± 92.895  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        492.500     ± 20.802  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        407.302     ± 13.302  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2855.769    ± 360.754  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2199.043    ± 170.828  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4558.415     ± 21.805  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     309094.610    ± 372.162  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     312207.241    ± 993.377  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     332918.790   ± 3332.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     334442.959   ± 2062.925  ops/s
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
