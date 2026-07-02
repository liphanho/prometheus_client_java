# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-02T07:16:42Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.65K | ± 863.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 425.53 | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 171.74 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.41K | ± 1.03K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 12.80 | ops/s | 9.9x slower |
| simpleclientInc | 6.58K | ± 184.20 | ops/s | 10.0x slower |
| simpleclientAdd | 6.11K | ± 285.63 | ops/s | 11x slower |
| openTelemetryAdd | 1.58K | ± 226.27 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.45K | ± 186.36 | ops/s | 45x slower |
| openTelemetryInc | 1.24K | ± 60.01 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 72.32 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 18.87 | ops/s | 1.1x slower |
| prometheusNative | 3.14K | ± 48.72 | ops/s | 1.6x slower |
| openTelemetryClassic | 728.14 | ± 29.03 | ops/s | 6.9x slower |
| openTelemetryExponential | 549.61 | ± 7.61 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.61K | ± 4.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.99K | ± 6.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.12K | ± 2.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.83K | ± 5.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48414.730   ± 1029.502  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1577.543    ± 226.267  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1237.349     ± 60.015  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1449.500    ± 186.362  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51489.231    ± 171.736  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65649.511    ± 863.140  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56887.406    ± 425.531  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6110.896    ± 285.633  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.511    ± 184.196  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6606.748     ± 12.800  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        728.138     ± 29.025  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.611      ± 7.606  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5042.930     ± 72.324  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3140.975     ± 48.719  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4504.959     ± 18.872  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507828.089   ± 5982.331  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512124.870   ± 2227.690  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524989.562   ± 6330.439  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537609.819   ± 4548.929  ops/s
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
