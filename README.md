# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T06:31:50Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.79K | ± 124.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.76K | ± 458.61 | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 131.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.24K | ± 8.17K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.50K | ± 127.63 | ops/s | 10x slower |
| simpleclientInc | 6.44K | ± 313.05 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 204.28 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 197.27 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.32K | ± 168.60 | ops/s | 50x slower |
| openTelemetryAdd | 1.27K | ± 30.43 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 15.90 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 32.80 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 180.60 | ops/s | 1.8x slower |
| openTelemetryClassic | 679.77 | ± 18.05 | ops/s | 8.1x slower |
| openTelemetryExponential | 560.19 | ± 32.57 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.46K | ± 5.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.07K | ± 11.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.74K | ± 8.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.54K | ± 3.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44244.666   ± 8171.863  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1273.101     ± 30.431  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1376.516    ± 197.269  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.172    ± 168.600  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51322.816    ± 131.603  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65785.463    ± 124.661  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55755.333    ± 458.615  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6354.737    ± 204.277  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6435.683    ± 313.053  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6499.506    ± 127.629  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.773     ± 18.052  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.185     ± 32.574  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5491.265     ± 15.901  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3066.396    ± 180.603  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.029     ± 32.803  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509535.588   ± 3549.507  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514739.636   ± 8554.800  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524070.035  ± 11559.553  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535459.856   ± 5933.044  ops/s
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
