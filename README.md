# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-24T07:24:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.55K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 331.75 | ops/s | 1.2x slower |
| prometheusAdd | 50.59K | ± 1.53K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.25K | ± 10.63K | ops/s | 1.6x slower |
| simpleclientNoLabelsInc | 6.62K | ± 10.60 | ops/s | 9.9x slower |
| simpleclientInc | 6.60K | ± 174.18 | ops/s | 9.9x slower |
| simpleclientAdd | 6.47K | ± 31.78 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 266.24 | ops/s | 45x slower |
| openTelemetryInc | 1.19K | ± 58.41 | ops/s | 55x slower |
| openTelemetryIncNoLabels | 1.16K | ± 42.55 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.13K | ± 19.43 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 27.70 | ops/s | 1.1x slower |
| prometheusNative | 3.13K | ± 41.77 | ops/s | 1.6x slower |
| openTelemetryClassic | 719.13 | ± 30.71 | ops/s | 7.1x slower |
| openTelemetryExponential | 531.93 | ± 16.18 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 531.22K | ± 5.33K | ops/s | **fastest** |
| prometheusWriteToNull | 528.21K | ± 7.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.14K | ± 8.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.27K | ± 4.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42249.590  ± 10626.132  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1456.229    ± 266.245  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1193.720     ± 58.413  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1158.273     ± 42.554  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50589.963   ± 1526.683  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65545.015   ± 1384.132  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56909.290    ± 331.747  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6467.660     ± 31.779  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6597.202    ± 174.178  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6618.293     ± 10.599  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.134     ± 30.711  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.925     ± 16.182  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5134.953     ± 19.435  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3128.002     ± 41.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.828     ± 27.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507269.717   ± 4017.765  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512142.564   ± 8320.108  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531220.917   ± 5333.355  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528205.507   ± 7513.504  ops/s
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
