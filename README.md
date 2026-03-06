# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-06T05:27:04Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.80K | ± 124.57 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.70K | ± 459.39 | ops/s | 1.2x slower |
| prometheusAdd | 51.26K | ± 651.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.95K | ± 2.04K | ops/s | 1.3x slower |
| simpleclientInc | 6.73K | ± 39.45 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.69K | ± 19.75 | ops/s | 9.8x slower |
| simpleclientAdd | 6.28K | ± 219.68 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.34K | ± 159.01 | ops/s | 49x slower |
| openTelemetryInc | 1.34K | ± 124.79 | ops/s | 49x slower |
| openTelemetryAdd | 1.27K | ± 64.90 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 50.09 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 63.75 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 203.08 | ops/s | 1.8x slower |
| openTelemetryClassic | 691.75 | ± 36.68 | ops/s | 7.6x slower |
| openTelemetryExponential | 552.52 | ± 27.10 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.94K | ± 6.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 538.92K | ± 5.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 524.38K | ± 6.70K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 521.34K | ± 3.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49954.833   ± 2039.457  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1270.471     ± 64.897  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1335.994    ± 124.791  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1338.330    ± 159.011  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51258.964    ± 651.010  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65796.186    ± 124.568  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56698.160    ± 459.390  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6275.369    ± 219.684  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6726.281     ± 39.446  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6690.175     ± 19.746  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.746     ± 36.675  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.518     ± 27.103  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5285.350     ± 50.090  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.337    ± 203.076  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4554.735     ± 63.750  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521343.968   ± 3410.139  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524382.976   ± 6700.385  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     538917.506   ± 5182.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551935.798   ± 6830.203  ops/s
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
