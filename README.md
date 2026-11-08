# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-08T09:56:41Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.48K | ± 567.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 511.88 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 76.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.78K | ± 1.94K | ops/s | 1.3x slower |
| simpleclientInc | 6.47K | ± 195.13 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.32K | ± 206.58 | ops/s | 11x slower |
| simpleclientAdd | 6.11K | ± 220.32 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 246.09 | ops/s | 47x slower |
| openTelemetryInc | 1.30K | ± 45.78 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.22K | ± 5.14 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 25.57 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 17.57 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 183.20 | ops/s | 1.9x slower |
| openTelemetryClassic | 700.07 | ± 42.00 | ops/s | 8.0x slower |
| openTelemetryExponential | 524.55 | ± 15.99 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.45K | ± 4.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.73K | ± 5.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.44K | ± 4.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.34K | ± 3.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49779.545   ± 1943.510  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1427.998    ± 246.091  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.774     ± 45.783  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1216.157      ± 5.137  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51268.980     ± 76.505  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66480.644    ± 567.163  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56977.843    ± 511.878  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6112.626    ± 220.324  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6466.613    ± 195.129  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6324.894    ± 206.584  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.066     ± 42.005  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.548     ± 15.988  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5607.211     ± 25.566  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2951.841    ± 183.205  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4352.599     ± 17.568  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465339.429   ± 3747.004  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470443.661   ± 4755.683  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476729.041   ± 5169.562  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492449.330   ± 4429.199  ops/s
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
