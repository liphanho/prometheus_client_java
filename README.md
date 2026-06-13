# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-13T07:34:16Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.45K | ± 1.90K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 1.04K | ops/s | 1.2x slower |
| prometheusAdd | 48.33K | ± 306.37 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.16K | ± 70.48 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.25K | ± 17.68 | ops/s | 9.5x slower |
| simpleclientInc | 6.19K | ± 107.72 | ops/s | 9.6x slower |
| simpleclientAdd | 5.86K | ± 184.98 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 98.36 | ops/s | 41x slower |
| openTelemetryInc | 1.43K | ± 133.44 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.28K | ± 76.15 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.39K | ± 12.45 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 55.66 | ops/s | 1.0x slower |
| prometheusNative | 3.00K | ± 91.21 | ops/s | 1.5x slower |
| openTelemetryClassic | 597.66 | ± 18.08 | ops/s | 7.4x slower |
| openTelemetryExponential | 488.60 | ± 15.39 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 640.20K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 629.26K | ± 4.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 608.03K | ± 4.92K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 594.33K | ± 3.03K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44158.529     ± 70.476  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1440.442     ± 98.364  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1427.314    ± 133.439  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1284.887     ± 76.154  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48334.071    ± 306.366  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59450.674   ± 1903.088  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51470.928   ± 1042.652  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5858.691    ± 184.983  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6192.558    ± 107.720  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6254.859     ± 17.681  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        597.663     ± 18.083  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        488.600     ± 15.392  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4393.904     ± 12.455  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3004.974     ± 91.206  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4369.972     ± 55.658  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     594327.949   ± 3032.868  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     608029.340   ± 4921.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     629262.442   ± 4138.385  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     640202.123   ± 3632.560  ops/s
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
