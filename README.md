# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-08T08:01:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 435.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 546.40 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 233.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.10K | ± 1.55K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 8.08 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 198.24 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 55.59 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 207.00 | ops/s | 47x slower |
| openTelemetryInc | 1.23K | ± 46.58 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.19K | ± 50.98 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 33.33 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 64.79 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 16.34 | ops/s | 1.7x slower |
| openTelemetryClassic | 700.28 | ± 14.94 | ops/s | 7.5x slower |
| openTelemetryExponential | 548.41 | ± 10.00 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.70K | ± 6.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.02K | ± 7.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.22K | ± 2.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.34K | ± 4.99K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48098.711   ± 1546.407  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1413.073    ± 206.997  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1226.847     ± 46.581  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.344     ± 50.975  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51291.555    ± 233.015  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66065.540    ± 435.390  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56748.211    ± 546.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6014.130     ± 55.590  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6673.559      ± 8.078  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6378.158    ± 198.239  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.283     ± 14.945  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.414     ± 10.001  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5256.832     ± 33.335  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3145.273     ± 16.339  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.942     ± 64.792  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524343.135   ± 4990.222  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536224.827   ± 2368.093  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548017.930   ± 7658.770  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548699.476   ± 6893.998  ops/s
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
