# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-27T11:51:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6975P-C, 4 cores, 15 GB RAM
- **OS:** Linux 7.0.0-1018-aws

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 34.12K | ± 226.36 | ops/s | **fastest** |
| prometheusInc | 33.26K | ± 211.57 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 33.17K | ± 550.09 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 31.85K | ± 128.16 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.56K | ± 42.43 | ops/s | 4.5x slower |
| simpleclientAdd | 7.54K | ± 110.33 | ops/s | 4.5x slower |
| simpleclientInc | 7.53K | ± 48.16 | ops/s | 4.5x slower |
| openTelemetryInc | 954.58 | ± 104.33 | ops/s | 36x slower |
| openTelemetryAdd | 949.54 | ± 58.10 | ops/s | 36x slower |
| openTelemetryIncNoLabels | 906.25 | ± 43.81 | ops/s | 38x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.27K | ± 27.49 | ops/s | **fastest** |
| prometheusClassic | 2.64K | ± 201.44 | ops/s | 2.0x slower |
| prometheusNative | 1.97K | ± 141.81 | ops/s | 2.7x slower |
| openTelemetryClassic | 364.52 | ± 52.71 | ops/s | 14x slower |
| openTelemetryExponential | 313.86 | ± 23.42 | ops/s | 17x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 439.04K | ± 5.68K | ops/s | **fastest** |
| prometheusWriteToNull | 429.01K | ± 2.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 416.00K | ± 6.74K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 405.48K | ± 4.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      33173.065    ± 550.089  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        949.544     ± 58.101  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        954.585    ± 104.325  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        906.251     ± 43.809  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      34121.714    ± 226.358  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      33255.800    ± 211.565  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31852.839    ± 128.159  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7539.493    ± 110.326  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7527.253     ± 48.160  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7562.310     ± 42.432  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        364.518     ± 52.706  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        313.862     ± 23.419  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2641.325    ± 201.437  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1971.860    ± 141.810  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5266.252     ± 27.493  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     416003.786   ± 6742.187  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     405482.101   ± 4435.390  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     439041.111   ± 5683.086  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     429012.716   ± 2447.643  ops/s
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
