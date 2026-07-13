# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-13T06:54:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.53K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.63K | ± 3.20K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.36K | ± 1.78K | ops/s | 1.3x slower |
| prometheusAdd | 43.73K | ± 12.22K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.53K | ± 135.11 | ops/s | 10x slower |
| simpleclientInc | 6.44K | ± 185.88 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 230.14 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 173.39 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 19.55 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 37.30 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.15K | ± 123.06 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 71.10 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 120.18 | ops/s | 1.7x slower |
| openTelemetryClassic | 696.39 | ± 35.71 | ops/s | 7.4x slower |
| openTelemetryExponential | 548.11 | ± 13.40 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.08K | ± 12.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.41K | ± 12.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.78K | ± 22.93K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 471.92K | ± 10.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49359.936   ± 1784.499  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1258.087     ± 19.546  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1346.525    ± 173.395  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1233.160     ± 37.305  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      43729.144  ± 12223.904  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65525.391   ± 1422.552  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54630.420   ± 3202.754  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6324.963    ± 230.141  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6444.493    ± 185.880  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6526.690    ± 135.110  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.395     ± 35.711  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.115     ± 13.399  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5151.967    ± 123.060  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.383    ± 120.182  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4400.845     ± 71.101  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471917.896  ± 10073.038  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479776.955  ± 22927.059  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492408.376  ± 12025.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509077.768  ± 12110.019  ops/s
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
