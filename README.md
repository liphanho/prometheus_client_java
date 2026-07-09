# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-09T07:22:15Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.01K | ± 1.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 110.02 | ops/s | 1.1x slower |
| prometheusAdd | 51.14K | ± 329.57 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 58.37 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.38K | ± 186.54 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 258.54 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 267.63 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.44K | ± 165.06 | ops/s | 45x slower |
| openTelemetryInc | 1.27K | ± 38.64 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 209.81 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 69.92 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 190.55 | ops/s | 1.6x slower |
| openTelemetryClassic | 694.25 | ± 30.73 | ops/s | 7.4x slower |
| openTelemetryExponential | 557.14 | ± 18.54 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.26K | ± 11.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.89K | ± 4.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 525.98K | ± 6.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 523.06K | ± 1.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48248.006   ± 1507.060  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1462.176    ± 267.628  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1267.225     ± 38.645  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1437.918    ± 165.060  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51142.778    ± 329.569  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65005.645   ± 1248.460  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57037.672    ± 110.023  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6299.596    ± 258.544  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6651.843     ± 58.367  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6377.830    ± 186.537  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.255     ± 30.731  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.141     ± 18.536  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5138.405    ± 209.813  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3171.000    ± 190.547  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.893     ± 69.918  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     523058.489   ± 1758.837  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     525977.355   ± 6938.779  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531891.254   ± 4559.320  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536262.865  ± 11861.876  ops/s
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
