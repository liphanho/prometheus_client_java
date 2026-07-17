# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-17T06:31:05Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.24K | ± 487.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.28K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 48.04K | ± 581.96 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.57K | ± 296.35 | ops/s | 1.3x slower |
| simpleclientInc | 6.24K | ± 119.20 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.09K | ± 233.99 | ops/s | 9.7x slower |
| simpleclientAdd | 6.03K | ± 144.45 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.52K | ± 60.86 | ops/s | 39x slower |
| openTelemetryAdd | 1.47K | ± 116.27 | ops/s | 40x slower |
| openTelemetryInc | 1.40K | ± 43.44 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 456.52 | ops/s | **fastest** |
| simpleclient | 4.66K | ± 35.68 | ops/s | 1.1x slower |
| prometheusNative | 3.20K | ± 37.07 | ops/s | 1.7x slower |
| openTelemetryClassic | 614.12 | ± 31.89 | ops/s | 8.6x slower |
| openTelemetryExponential | 528.86 | ± 13.45 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 617.58K | ± 5.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 605.43K | ± 4.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 590.94K | ± 2.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 575.42K | ± 4.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44568.095    ± 296.354  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1465.364    ± 116.269  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1402.480     ± 43.442  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1520.467     ± 60.861  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48040.854    ± 581.957  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59241.531    ± 487.136  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51279.858   ± 1085.257  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6034.844    ± 144.448  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6237.612    ± 119.203  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6091.871    ± 233.993  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        614.124     ± 31.893  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        528.863     ± 13.447  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5301.653    ± 456.520  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3203.312     ± 37.072  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4657.064     ± 35.680  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     575420.727   ± 4469.423  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     590941.868   ± 2889.408  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     605433.365   ± 4908.901  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     617577.899   ± 5416.729  ops/s
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
