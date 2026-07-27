# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-27T07:07:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.80K | ± 1.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.06K | ± 1.23K | ops/s | 1.2x slower |
| prometheusAdd | 50.39K | ± 1.73K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.53K | ± 1.97K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 13.64 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.46K | ± 214.54 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 170.82 | ops/s | 10x slower |
| openTelemetryAdd | 1.53K | ± 190.67 | ops/s | 42x slower |
| openTelemetryInc | 1.33K | ± 130.23 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.32K | ± 172.88 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 26.15 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 54.91 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 48.88 | ops/s | 1.8x slower |
| openTelemetryClassic | 698.05 | ± 28.95 | ops/s | 7.5x slower |
| openTelemetryExponential | 566.86 | ± 18.35 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 521.21K | ± 8.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.73K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 506.59K | ± 6.18K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 496.50K | ± 4.15K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49527.780   ± 1973.283  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1532.164    ± 190.667  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1329.996    ± 130.233  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1317.147    ± 172.884  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50389.070   ± 1730.049  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64795.097   ± 1397.576  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56057.681   ± 1230.309  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6188.358    ± 170.817  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6693.096     ± 13.636  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6461.448    ± 214.543  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.052     ± 28.951  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.857     ± 18.349  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5230.960     ± 26.148  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2903.415     ± 48.885  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4428.633     ± 54.911  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     496496.850   ± 4153.009  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     506588.408   ± 6180.274  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513729.813   ± 3937.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     521212.971   ± 8738.049  ops/s
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
