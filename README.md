# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-21T04:19:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.87K | ± 349.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 410.78 | ops/s | 1.2x slower |
| prometheusAdd | 50.66K | ± 352.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.07K | ± 1.42K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 51.22 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 278.56 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 223.80 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 176.10 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.39K | ± 164.44 | ops/s | 47x slower |
| openTelemetryAdd | 1.29K | ± 41.50 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 61.51 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 31.48 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 139.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 682.97 | ± 21.52 | ops/s | 7.7x slower |
| openTelemetryExponential | 572.99 | ± 31.47 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.72K | ± 7.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.95K | ± 3.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.97K | ± 2.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.22K | ± 3.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50070.067   ± 1424.939  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1291.214     ± 41.500  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1460.894    ± 176.097  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1393.140    ± 164.437  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50656.142    ± 352.459  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65871.886    ± 349.120  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56829.465    ± 410.779  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6314.864    ± 223.802  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6650.767     ± 51.221  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.386    ± 278.563  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.965     ± 21.518  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.994     ± 31.468  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5267.448     ± 61.506  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3050.936    ± 139.642  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4489.878     ± 31.475  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469221.579   ± 3509.248  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480971.917   ± 2132.672  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493949.717   ± 3205.852  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496715.814   ± 7014.643  ops/s
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
