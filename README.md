# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-23T08:20:03Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.96K | ± 323.89 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.52K | ± 779.33 | ops/s | 1.2x slower |
| prometheusAdd | 50.47K | ± 1.43K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.19K | ± 7.20K | ops/s | 1.5x slower |
| simpleclientInc | 6.68K | ± 15.55 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 123.81 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 206.97 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.30K | ± 155.87 | ops/s | 51x slower |
| openTelemetryAdd | 1.23K | ± 36.86 | ops/s | 54x slower |
| openTelemetryInc | 1.23K | ± 10.60 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 59.13 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 74.36 | ops/s | 1.2x slower |
| prometheusNative | 3.10K | ± 35.70 | ops/s | 1.7x slower |
| openTelemetryClassic | 644.67 | ± 18.96 | ops/s | 8.1x slower |
| openTelemetryExponential | 549.08 | ± 24.55 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 517.87K | ± 4.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 511.53K | ± 6.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 498.83K | ± 4.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.93K | ± 8.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43188.825   ± 7196.170  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1232.750     ± 36.856  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1231.937     ± 10.598  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1296.471    ± 155.872  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50473.915   ± 1432.190  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65957.907    ± 323.887  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56519.755    ± 779.330  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6157.837    ± 206.967  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6683.530     ± 15.551  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6494.280    ± 123.810  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        644.675     ± 18.959  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.085     ± 24.551  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5236.571     ± 59.131  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3096.201     ± 35.702  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.510     ± 74.362  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488929.079   ± 8317.693  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     498828.065   ± 4546.350  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     511529.612   ± 6052.645  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     517872.709   ± 4489.289  ops/s
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
