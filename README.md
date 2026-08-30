# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-30T09:15:00Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.04K | ± 1.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.77K | ± 308.31 | ops/s | 1.1x slower |
| prometheusAdd | 51.39K | ± 221.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.55K | ± 453.61 | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 58.41 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.40K | ± 170.32 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 269.55 | ops/s | 10x slower |
| openTelemetryAdd | 1.49K | ± 240.02 | ops/s | 44x slower |
| openTelemetryInc | 1.25K | ± 38.55 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 1.93 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 217.06 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 54.07 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 106.77 | ops/s | 1.7x slower |
| openTelemetryClassic | 674.27 | ± 34.55 | ops/s | 7.8x slower |
| openTelemetryExponential | 567.10 | ± 7.64 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.39K | ± 3.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 522.33K | ± 13.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.28K | ± 4.35K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 500.37K | ± 4.78K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47553.932    ± 453.607  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1491.973    ± 240.018  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1249.935     ± 38.554  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1228.650      ± 1.929  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51394.175    ± 221.064  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65036.532   ± 1293.369  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56771.352    ± 308.314  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6266.146    ± 269.545  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6664.570     ± 58.409  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6400.528    ± 170.319  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.266     ± 34.549  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.097      ± 7.638  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5284.007    ± 217.058  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3056.348    ± 106.773  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4471.488     ± 54.075  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500372.394   ± 4784.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505275.958   ± 4352.696  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     522329.364  ± 13219.530  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532386.489   ± 3902.015  ops/s
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
