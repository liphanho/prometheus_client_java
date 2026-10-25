# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-25T08:36:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.80K | ± 1.37K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.08K | ± 428.51 | ops/s | 1.1x slower |
| prometheusAdd | 48.00K | ± 429.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.70K | ± 1.42K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.24K | ± 40.38 | ops/s | 9.6x slower |
| simpleclientInc | 6.10K | ± 85.18 | ops/s | 9.8x slower |
| simpleclientAdd | 5.96K | ± 293.22 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.37K | ± 77.46 | ops/s | 44x slower |
| openTelemetryAdd | 1.34K | ± 102.72 | ops/s | 45x slower |
| openTelemetryInc | 1.26K | ± 43.35 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 52.61 | ops/s | **fastest** |
| prometheusClassic | 4.29K | ± 745.90 | ops/s | 1.0x slower |
| prometheusNative | 3.15K | ± 37.60 | ops/s | 1.4x slower |
| openTelemetryClassic | 583.68 | ± 9.87 | ops/s | 7.6x slower |
| openTelemetryExponential | 510.29 | ± 18.46 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 645.72K | ± 2.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 629.97K | ± 4.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 601.69K | ± 4.61K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 597.67K | ± 4.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43695.596   ± 1415.433  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1343.049    ± 102.722  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1256.012     ± 43.351  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1371.017     ± 77.458  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48004.308    ± 429.055  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59801.864   ± 1366.886  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52080.494    ± 428.509  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5956.793    ± 293.223  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6100.369     ± 85.178  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6240.317     ± 40.375  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        583.685      ± 9.868  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        510.290     ± 18.458  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4289.614    ± 745.903  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3145.236     ± 37.597  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4422.163     ± 52.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     597668.861   ± 4168.568  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     601689.644   ± 4608.046  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     629968.358   ± 4939.635  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     645718.159   ± 2469.180  ops/s
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
