# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-18T05:49:41Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.65K | ± 3.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 580.20 | ops/s | 1.1x slower |
| prometheusAdd | 47.91K | ± 404.93 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.64K | ± 1.22K | ops/s | 1.4x slower |
| simpleclientInc | 6.29K | ± 75.09 | ops/s | 9.2x slower |
| simpleclientAdd | 6.17K | ± 45.81 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 5.96K | ± 258.41 | ops/s | 9.7x slower |
| openTelemetryIncNoLabels | 1.44K | ± 78.39 | ops/s | 40x slower |
| openTelemetryAdd | 1.38K | ± 58.52 | ops/s | 42x slower |
| openTelemetryInc | 1.33K | ± 52.09 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 59.66 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 127.15 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 92.14 | ops/s | 1.8x slower |
| openTelemetryClassic | 611.82 | ± 25.39 | ops/s | 8.9x slower |
| openTelemetryExponential | 512.13 | ± 12.57 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 604.24K | ± 12.66K | ops/s | **fastest** |
| prometheusWriteToNull | 592.65K | ± 6.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 573.35K | ± 10.20K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 569.70K | ± 9.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42637.331   ± 1218.038  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1378.360     ± 58.516  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1332.478     ± 52.093  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1438.575     ± 78.393  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47912.272    ± 404.927  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57654.027   ± 3766.716  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51396.031    ± 580.201  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6165.816     ± 45.808  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6291.873     ± 75.090  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5959.603    ± 258.407  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.817     ± 25.385  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.126     ± 12.566  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5465.340     ± 59.662  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3006.951     ± 92.144  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4352.555    ± 127.154  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     573354.927  ± 10196.056  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     569704.381   ± 9569.988  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     604241.114  ± 12659.038  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     592650.050   ± 6979.969  ops/s
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
