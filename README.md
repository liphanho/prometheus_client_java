# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T05:42:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.48K | ± 1.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 442.12 | ops/s | 1.1x slower |
| prometheusAdd | 50.54K | ± 1.22K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 1.40K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 57.48 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.50K | ± 194.69 | ops/s | 9.9x slower |
| simpleclientAdd | 6.33K | ± 183.02 | ops/s | 10x slower |
| openTelemetryInc | 1.30K | ± 26.44 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.23K | ± 49.13 | ops/s | 53x slower |
| openTelemetryAdd | 1.22K | ± 74.99 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 104.25 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 88.86 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 144.44 | ops/s | 1.7x slower |
| openTelemetryClassic | 655.52 | ± 31.29 | ops/s | 7.7x slower |
| openTelemetryExponential | 558.52 | ± 28.83 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.23K | ± 5.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.85K | ± 14.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.44K | ± 6.13K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 510.09K | ± 2.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48474.552   ± 1396.985  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1215.638     ± 74.986  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1296.836     ± 26.439  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1227.151     ± 49.128  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50540.491   ± 1223.179  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64481.049   ± 1435.363  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56928.335    ± 442.119  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6330.985    ± 183.019  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6663.092     ± 57.480  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6500.299    ± 194.690  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        655.523     ± 31.291  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.520     ± 28.831  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5062.796    ± 104.251  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3007.480    ± 144.441  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4394.477     ± 88.859  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510086.714   ± 2723.000  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512443.264   ± 6126.026  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531854.277  ± 14400.141  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538232.364   ± 5069.331  ops/s
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
