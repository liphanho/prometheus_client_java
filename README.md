# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-16T10:21:35Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6975P-C, 4 cores, 15 GB RAM
- **OS:** Linux 7.0.0-1014-aws

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 34.17K | ± 163.17 | ops/s | **fastest** |
| prometheusInc | 33.19K | ± 79.49 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 32.93K | ± 849.01 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 32.04K | ± 70.62 | ops/s | 1.1x slower |
| simpleclientAdd | 7.61K | ± 92.49 | ops/s | 4.5x slower |
| simpleclientInc | 7.55K | ± 85.77 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 7.51K | ± 71.62 | ops/s | 4.5x slower |
| openTelemetryInc | 970.73 | ± 57.82 | ops/s | 35x slower |
| openTelemetryIncNoLabels | 965.34 | ± 74.04 | ops/s | 35x slower |
| openTelemetryAdd | 884.03 | ± 87.85 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.21K | ± 103.96 | ops/s | **fastest** |
| prometheusClassic | 2.86K | ± 330.56 | ops/s | 1.8x slower |
| prometheusNative | 2.06K | ± 120.27 | ops/s | 2.5x slower |
| openTelemetryClassic | 384.25 | ± 27.50 | ops/s | 14x slower |
| openTelemetryExponential | 301.20 | ± 25.38 | ops/s | 17x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 444.10K | ± 6.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 442.24K | ± 11.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 422.20K | ± 9.27K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 409.03K | ± 2.97K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      32934.761    ± 849.014  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        884.025     ± 87.851  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        970.726     ± 57.824  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        965.344     ± 74.039  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      34166.097    ± 163.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      33194.024     ± 79.488  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      32041.286     ± 70.620  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7607.620     ± 92.488  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7545.177     ± 85.771  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7514.573     ± 71.620  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        384.254     ± 27.499  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        301.205     ± 25.380  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2856.503    ± 330.564  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2062.868    ± 120.272  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5213.947    ± 103.963  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     422201.205   ± 9271.430  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     409028.089   ± 2970.455  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     442241.734  ± 11691.823  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     444103.113   ± 6170.587  ops/s
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
