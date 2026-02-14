# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-14T05:27:50Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.70K | ± 558.60 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 941.67 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 424.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.54K | ± 1.46K | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 28.01 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.69K | ± 17.90 | ops/s | 10.0x slower |
| simpleclientAdd | 6.20K | ± 80.31 | ops/s | 11x slower |
| openTelemetryAdd | 1.39K | ± 238.93 | ops/s | 48x slower |
| openTelemetryInc | 1.32K | ± 101.17 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.30K | ± 164.82 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 45.85 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 28.31 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 154.48 | ops/s | 1.7x slower |
| openTelemetryClassic | 679.80 | ± 16.21 | ops/s | 7.7x slower |
| openTelemetryExponential | 565.37 | ± 35.18 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.45K | ± 5.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.96K | ± 5.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.94K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 500.36K | ± 7.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49536.717   ± 1460.126  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1388.292    ± 238.934  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1317.231    ± 101.171  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1297.216    ± 164.816  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51283.988    ± 424.707  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66697.771    ± 558.597  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56237.359    ± 941.671  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6198.880     ± 80.313  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6756.198     ± 28.008  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6694.488     ± 17.905  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.803     ± 16.213  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.375     ± 35.183  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5213.766     ± 45.845  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3037.904    ± 154.476  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4529.271     ± 28.313  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500360.342   ± 7095.360  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512941.734   ± 3231.501  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523964.710   ± 5725.433  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529449.421   ± 5902.720  ops/s
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
