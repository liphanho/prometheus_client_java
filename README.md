# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-29T05:54:53Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.31K | ± 1.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 335.33 | ops/s | 1.1x slower |
| prometheusAdd | 51.07K | ± 154.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.51K | ± 1.87K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.58K | ± 74.80 | ops/s | 9.9x slower |
| simpleclientInc | 6.48K | ± 166.24 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 92.51 | ops/s | 11x slower |
| openTelemetryInc | 1.35K | ± 112.82 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.28K | ± 198.58 | ops/s | 51x slower |
| openTelemetryAdd | 1.24K | ± 83.36 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.07K | ± 94.69 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 42.98 | ops/s | 1.1x slower |
| prometheusNative | 3.09K | ± 40.13 | ops/s | 1.6x slower |
| openTelemetryClassic | 704.20 | ± 37.50 | ops/s | 7.2x slower |
| openTelemetryExponential | 554.98 | ± 32.10 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.08K | ± 8.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.14K | ± 19.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 493.44K | ± 11.08K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 475.74K | ± 27.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49513.983   ± 1873.371  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1236.636     ± 83.355  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1348.876    ± 112.824  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1279.333    ± 198.583  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51072.873    ± 154.179  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65305.665   ± 1440.255  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56934.247    ± 335.333  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6013.318     ± 92.506  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6478.800    ± 166.236  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6584.321     ± 74.804  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.203     ± 37.501  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.976     ± 32.101  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5071.633     ± 94.694  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3093.326     ± 40.132  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4450.622     ± 42.984  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     493444.537  ± 11084.028  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475743.428  ± 27825.908  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506135.496  ± 19522.961  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527083.320   ± 8575.284  ops/s
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
