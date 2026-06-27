# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-27T07:10:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.83K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 64.73K | ± 698.62 | ops/s | 1.0x slower |
| prometheusAdd | 59.30K | ± 2.77K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 55.64K | ± 8.08K | ops/s | 1.2x slower |
| simpleclientInc | 10.61K | ± 314.81 | ops/s | 6.3x slower |
| simpleclientAdd | 10.38K | ± 142.59 | ops/s | 6.4x slower |
| simpleclientNoLabelsInc | 10.36K | ± 311.38 | ops/s | 6.4x slower |
| openTelemetryAdd | 2.28K | ± 146.98 | ops/s | 29x slower |
| openTelemetryIncNoLabels | 2.01K | ± 200.25 | ops/s | 33x slower |
| openTelemetryInc | 1.82K | ± 103.99 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.34K | ± 34.30 | ops/s | **fastest** |
| simpleclient | 7.12K | ± 64.43 | ops/s | 1.0x slower |
| prometheusNative | 5.16K | ± 562.01 | ops/s | 1.4x slower |
| openTelemetryClassic | 850.68 | ± 35.45 | ops/s | 8.6x slower |
| openTelemetryExponential | 669.35 | ± 17.36 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 790.20K | ± 46.99K | ops/s | **fastest** |
| openMetricsWriteToNull | 767.23K | ± 47.40K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 762.81K | ± 33.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 705.23K | ± 8.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55638.279   ± 8078.925  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2281.357    ± 146.980  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1818.835    ± 103.993  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2006.411    ± 200.247  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59300.153   ± 2767.680  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66826.370   ± 1021.335  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64733.253    ± 698.620  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10380.742    ± 142.586  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10605.223    ± 314.807  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10362.032    ± 311.382  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        850.681     ± 35.454  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        669.349     ± 17.356  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7344.750     ± 34.302  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5155.660    ± 562.011  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7119.523     ± 64.426  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     705226.300   ± 8495.195  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     767233.528  ± 47403.767  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     762810.044  ± 33986.270  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     790195.317  ± 46989.983  ops/s
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
