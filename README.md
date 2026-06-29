# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-29T08:05:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.08K | ± 298.30 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.94K | ± 751.06 | ops/s | 1.2x slower |
| prometheusAdd | 51.50K | ± 225.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.06K | ± 1.98K | ops/s | 1.3x slower |
| simpleclientInc | 6.63K | ± 47.16 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.51K | ± 122.65 | ops/s | 10x slower |
| simpleclientAdd | 6.37K | ± 141.81 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.47K | ± 226.72 | ops/s | 45x slower |
| openTelemetryInc | 1.27K | ± 50.50 | ops/s | 52x slower |
| openTelemetryAdd | 1.21K | ± 31.77 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 353.70 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 30.70 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 159.97 | ops/s | 1.8x slower |
| openTelemetryClassic | 703.20 | ± 21.41 | ops/s | 7.6x slower |
| openTelemetryExponential | 571.22 | ± 16.68 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.36K | ± 1.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.18K | ± 9.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.83K | ± 3.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.92K | ± 5.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49061.694   ± 1976.144  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1214.999     ± 31.766  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1272.053     ± 50.499  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1470.463    ± 226.718  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51498.887    ± 225.603  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66075.470    ± 298.297  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55937.609    ± 751.055  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6372.742    ± 141.809  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6634.764     ± 47.156  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6512.069    ± 122.655  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.199     ± 21.412  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.219     ± 16.681  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5338.012    ± 353.698  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2944.838    ± 159.973  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4416.147     ± 30.700  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506919.706   ± 5661.118  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508826.088   ± 3339.112  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526176.525   ± 9096.610  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526358.706   ± 1164.871  ops/s
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
