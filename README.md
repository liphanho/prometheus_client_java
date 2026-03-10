# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-10T05:27:37Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.68K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.97K | ± 1.24K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.18K | ± 1.58K | ops/s | 1.1x slower |
| prometheusAdd | 28.54K | ± 133.31 | ops/s | 1.1x slower |
| simpleclientInc | 7.02K | ± 98.72 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.78K | ± 309.95 | ops/s | 4.5x slower |
| simpleclientAdd | 6.67K | ± 217.56 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.41K | ± 156.81 | ops/s | 22x slower |
| openTelemetryInc | 1.40K | ± 143.66 | ops/s | 22x slower |
| openTelemetryAdd | 1.34K | ± 31.26 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 89.47 | ops/s | **fastest** |
| prometheusClassic | 2.96K | ± 213.69 | ops/s | 1.5x slower |
| prometheusNative | 2.33K | ± 101.24 | ops/s | 2.0x slower |
| openTelemetryClassic | 536.88 | ± 29.96 | ops/s | 8.5x slower |
| openTelemetryExponential | 400.73 | ± 26.27 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 336.38K | ± 2.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 332.00K | ± 4.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 304.64K | ± 3.05K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 301.37K | ± 4.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29176.112   ± 1578.605  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1337.293     ± 31.256  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1400.195    ± 143.656  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1408.600    ± 156.808  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28539.048    ± 133.310  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30680.605   ± 1264.255  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29973.184   ± 1237.478  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6670.144    ± 217.559  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7024.260     ± 98.722  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6776.416    ± 309.950  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        536.884     ± 29.962  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        400.731     ± 26.268  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2962.711    ± 213.688  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2332.871    ± 101.238  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4568.918     ± 89.468  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     301371.576   ± 4725.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     304641.780   ± 3046.457  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     331995.370   ± 4324.072  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     336379.386   ± 2847.738  ops/s
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
