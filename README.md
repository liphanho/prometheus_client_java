# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-11T05:01:01Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.74K | ± 726.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 134.21 | ops/s | 1.2x slower |
| prometheusAdd | 50.66K | ± 1.41K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.52K | ± 1.37K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 170.14 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.49K | ± 181.56 | ops/s | 10x slower |
| simpleclientAdd | 5.96K | ± 9.05 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 304.39 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 15.01 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.19K | ± 29.14 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 206.21 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 41.32 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 25.88 | ops/s | 1.7x slower |
| openTelemetryClassic | 673.53 | ± 18.55 | ops/s | 7.8x slower |
| openTelemetryExponential | 571.91 | ± 46.94 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.32K | ± 6.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.30K | ± 6.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 513.95K | ± 2.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.33K | ± 7.94K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48523.365   ± 1374.284  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1438.937    ± 304.395  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.748     ± 15.007  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1188.018     ± 29.145  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50659.361   ± 1410.590  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65738.647    ± 726.264  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57060.866    ± 134.212  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5963.190      ± 9.049  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.185    ± 170.137  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6486.656    ± 181.562  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.530     ± 18.545  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.909     ± 46.940  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5244.556    ± 206.214  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3148.092     ± 25.876  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4382.548     ± 41.316  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509326.869   ± 7943.931  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     513952.363   ± 2352.722  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523298.299   ± 6328.924  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534323.719   ± 6230.205  ops/s
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
