# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-28T11:09:00Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6975P-C, 4 cores, 15 GB RAM
- **OS:** Linux 7.0.0-1018-aws

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 34.62K | ± 705.95 | ops/s | **fastest** |
| prometheusNoLabelsInc | 34.12K | ± 430.26 | ops/s | 1.0x slower |
| prometheusAdd | 33.84K | ± 230.15 | ops/s | 1.0x slower |
| prometheusInc | 33.73K | ± 527.42 | ops/s | 1.0x slower |
| simpleclientNoLabelsInc | 7.51K | ± 27.01 | ops/s | 4.6x slower |
| simpleclientAdd | 7.48K | ± 42.90 | ops/s | 4.6x slower |
| simpleclientInc | 7.45K | ± 83.19 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 895.73 | ± 27.59 | ops/s | 39x slower |
| openTelemetryAdd | 895.17 | ± 16.51 | ops/s | 39x slower |
| openTelemetryInc | 883.08 | ± 37.13 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.26K | ± 19.10 | ops/s | **fastest** |
| prometheusClassic | 2.56K | ± 272.09 | ops/s | 2.1x slower |
| prometheusNative | 1.80K | ± 30.84 | ops/s | 2.9x slower |
| openTelemetryClassic | 365.24 | ± 17.70 | ops/s | 14x slower |
| openTelemetryExponential | 319.05 | ± 13.30 | ops/s | 16x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 444.22K | ± 3.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 441.24K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 416.81K | ± 5.39K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 411.12K | ± 3.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      34620.262    ± 705.946  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        895.174     ± 16.514  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        883.085     ± 37.126  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        895.733     ± 27.589  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      33842.559    ± 230.148  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      33725.720    ± 527.420  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      34123.478    ± 430.257  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7475.966     ± 42.897  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7454.264     ± 83.185  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7506.738     ± 27.008  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        365.238     ± 17.696  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        319.045     ± 13.299  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2555.785    ± 272.091  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1801.145     ± 30.840  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5260.729     ± 19.105  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     411116.912   ± 3085.165  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     416807.537   ± 5388.252  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     441240.498   ± 3433.674  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     444220.157   ± 3166.947  ops/s
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
