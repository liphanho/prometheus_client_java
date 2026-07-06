# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-06T07:53:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.88K | ± 114.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.76K | ± 384.72 | ops/s | 1.2x slower |
| prometheusAdd | 51.14K | ± 482.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.25K | ± 7.87K | ops/s | 1.5x slower |
| simpleclientInc | 6.55K | ± 151.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 211.26 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 296.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.57K | ± 246.14 | ops/s | 42x slower |
| openTelemetryInc | 1.39K | ± 157.34 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.32K | ± 167.57 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 133.58 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 20.56 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 200.04 | ops/s | 1.7x slower |
| openTelemetryClassic | 710.27 | ± 21.29 | ops/s | 7.5x slower |
| openTelemetryExponential | 572.84 | ± 34.28 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.81K | ± 3.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.22K | ± 9.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.46K | ± 3.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 517.74K | ± 6.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44249.659   ± 7869.590  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1568.564    ± 246.135  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1394.734    ± 157.336  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1319.895    ± 167.572  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51143.850    ± 482.858  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65875.103    ± 114.291  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56756.343    ± 384.717  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6127.901    ± 296.854  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.925    ± 151.940  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6344.308    ± 211.265  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.274     ± 21.288  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.837     ± 34.283  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5297.531    ± 133.580  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.451    ± 200.041  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4384.948     ± 20.557  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519457.926   ± 3805.060  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     517739.402   ± 6540.498  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533223.058   ± 9335.939  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541809.801   ± 3091.977  ops/s
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
