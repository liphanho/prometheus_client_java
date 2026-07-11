# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-11T06:30:41Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.32K | ± 325.44 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 413.73 | ops/s | 1.2x slower |
| prometheusAdd | 51.20K | ± 772.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.78K | ± 2.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 164.88 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 190.83 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 232.80 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 197.29 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.28K | ± 188.03 | ops/s | 52x slower |
| openTelemetryInc | 1.22K | ± 51.26 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 8.43 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 20.05 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 134.94 | ops/s | 1.7x slower |
| openTelemetryClassic | 673.86 | ± 5.55 | ops/s | 7.7x slower |
| openTelemetryExponential | 539.97 | ± 2.44 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 525.98K | ± 3.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 519.96K | ± 8.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.82K | ± 2.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.34K | ± 6.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48783.280   ± 2031.793  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1365.858    ± 197.293  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1222.344     ± 51.260  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1280.111    ± 188.028  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51202.924    ± 772.768  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66323.531    ± 325.437  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56925.058    ± 413.728  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6325.141    ± 232.801  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6585.536    ± 164.883  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6373.595    ± 190.829  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.863      ± 5.550  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.972      ± 2.444  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5209.385      ± 8.431  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3026.169    ± 134.945  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4516.762     ± 20.052  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508335.809   ± 6096.312  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518821.049   ± 2519.424  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     519959.619   ± 8158.130  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     525983.718   ± 3229.397  ops/s
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
