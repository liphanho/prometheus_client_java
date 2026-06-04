# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-04T07:59:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.89K | ± 56.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.84K | ± 784.20 | ops/s | 1.2x slower |
| prometheusAdd | 48.53K | ± 1.09K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 35.66K | ± 11.20K | ops/s | 1.7x slower |
| simpleclientNoLabelsInc | 6.28K | ± 13.30 | ops/s | 9.5x slower |
| simpleclientInc | 6.23K | ± 180.62 | ops/s | 9.6x slower |
| simpleclientAdd | 5.89K | ± 240.51 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 184.34 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.34K | ± 129.34 | ops/s | 45x slower |
| openTelemetryInc | 1.33K | ± 73.96 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 117.38 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 91.30 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 104.52 | ops/s | 1.8x slower |
| openTelemetryClassic | 628.14 | ± 40.93 | ops/s | 8.8x slower |
| openTelemetryExponential | 538.14 | ± 48.28 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 622.21K | ± 3.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 604.63K | ± 3.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 586.25K | ± 8.89K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 575.45K | ± 4.90K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      35655.195  ± 11201.499  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1407.225    ± 184.341  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1332.602     ± 73.958  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1340.148    ± 129.336  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48532.156   ± 1091.035  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59894.348     ± 56.756  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51844.936    ± 784.196  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5890.967    ± 240.505  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6233.973    ± 180.622  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6283.731     ± 13.303  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        628.141     ± 40.931  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.144     ± 48.278  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5530.305    ± 117.380  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3036.530    ± 104.517  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4563.987     ± 91.302  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     575452.683   ± 4898.956  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     586254.493   ± 8890.926  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     604628.525   ± 3260.884  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     622210.939   ± 3352.091  ops/s
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
