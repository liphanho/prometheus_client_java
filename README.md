# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-16T08:35:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.00K | ± 369.77 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.78K | ± 1.49K | ops/s | 1.0x slower |
| prometheusInc | 30.78K | ± 387.58 | ops/s | 1.0x slower |
| prometheusAdd | 30.02K | ± 120.12 | ops/s | 1.0x slower |
| simpleclientInc | 7.82K | ± 73.23 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.77K | ± 39.82 | ops/s | 4.0x slower |
| simpleclientAdd | 7.64K | ± 214.33 | ops/s | 4.1x slower |
| openTelemetryInc | 1.20K | ± 69.47 | ops/s | 26x slower |
| openTelemetryIncNoLabels | 1.16K | ± 81.19 | ops/s | 27x slower |
| openTelemetryAdd | 1.11K | ± 97.31 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.04K | ± 51.99 | ops/s | **fastest** |
| prometheusClassic | 2.84K | ± 345.49 | ops/s | 1.8x slower |
| prometheusNative | 2.20K | ± 154.39 | ops/s | 2.3x slower |
| openTelemetryClassic | 418.06 | ± 3.53 | ops/s | 12x slower |
| openTelemetryExponential | 340.82 | ± 4.14 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 331.71K | ± 4.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 329.51K | ± 3.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 307.88K | ± 4.35K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 306.81K | ± 2.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30783.141   ± 1491.490  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1110.332     ± 97.306  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1202.296     ± 69.473  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1160.339     ± 81.188  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      30015.581    ± 120.117  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30780.270    ± 387.582  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31004.181    ± 369.774  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7638.559    ± 214.328  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7824.747     ± 73.227  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7765.975     ± 39.820  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        418.064      ± 3.531  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        340.818      ± 4.136  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2841.444    ± 345.493  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2202.102    ± 154.386  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5044.826     ± 51.985  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     307884.299   ± 4350.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     306805.096   ± 2254.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     329511.572   ± 3470.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     331708.241   ± 4505.403  ops/s
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
