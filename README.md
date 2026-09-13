# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T08:30:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.85K | ± 2.72K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.91K | ± 199.31 | ops/s | 1.1x slower |
| prometheusAdd | 52.17K | ± 634.64 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.56K | ± 707.25 | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 166.94 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.64K | ± 225.22 | ops/s | 9.6x slower |
| simpleclientAdd | 6.28K | ± 162.41 | ops/s | 10x slower |
| openTelemetryAdd | 1.66K | ± 37.91 | ops/s | 38x slower |
| openTelemetryIncNoLabels | 1.51K | ± 126.09 | ops/s | 42x slower |
| openTelemetryInc | 1.49K | ± 151.83 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.68K | ± 109.99 | ops/s | **fastest** |
| simpleclient | 4.89K | ± 92.28 | ops/s | 1.2x slower |
| prometheusNative | 3.46K | ± 34.24 | ops/s | 1.6x slower |
| openTelemetryClassic | 653.44 | ± 25.29 | ops/s | 8.7x slower |
| openTelemetryExponential | 589.30 | ± 52.87 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 652.08K | ± 10.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 650.69K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 614.55K | ± 7.80K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 604.52K | ± 4.78K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48563.446    ± 707.254  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1664.135     ± 37.913  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1491.335    ± 151.829  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1505.831    ± 126.089  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      52166.203    ± 634.639  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63853.245   ± 2716.028  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55908.201    ± 199.313  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6282.900    ± 162.414  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6699.697    ± 166.938  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6637.075    ± 225.221  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        653.435     ± 25.291  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.297     ± 52.871  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5679.929    ± 109.993  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3458.455     ± 34.239  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4889.241     ± 92.280  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     604521.325   ± 4778.825  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     614552.693   ± 7796.503  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     650693.376   ± 4108.589  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     652079.772  ± 10259.129  ops/s
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
