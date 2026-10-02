# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T09:16:56Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.76K | ± 171.61 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 259.00 | ops/s | 1.2x slower |
| prometheusAdd | 50.92K | ± 729.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.26K | ± 1.05K | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 80.18 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.51K | ± 129.99 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 300.97 | ops/s | 11x slower |
| openTelemetryInc | 1.45K | ± 168.34 | ops/s | 45x slower |
| openTelemetryAdd | 1.29K | ± 38.16 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 3.21 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 61.92 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 69.27 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 204.81 | ops/s | 1.7x slower |
| openTelemetryClassic | 682.63 | ± 40.05 | ops/s | 7.7x slower |
| openTelemetryExponential | 554.93 | ± 34.30 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 526.77K | ± 4.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 518.30K | ± 5.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 502.27K | ± 3.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 498.14K | ± 1.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48260.271   ± 1053.645  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1291.018     ± 38.165  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1448.629    ± 168.336  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1201.573      ± 3.215  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50920.157    ± 729.853  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65758.244    ± 171.613  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56781.325    ± 258.997  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6117.113    ± 300.966  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6596.494     ± 80.179  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6510.498    ± 129.990  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.630     ± 40.053  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.932     ± 34.304  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5224.661     ± 61.924  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3081.402    ± 204.809  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.860     ± 69.275  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     498136.414   ± 1942.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     502267.891   ± 3325.943  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     518302.181   ± 5335.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526765.317   ± 4809.230  ops/s
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
