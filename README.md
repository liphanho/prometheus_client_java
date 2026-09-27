# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-27T08:57:03Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.14K | ± 618.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.07K | ± 254.88 | ops/s | 1.2x slower |
| prometheusAdd | 50.42K | ± 1.62K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.46K | ± 539.76 | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 165.85 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 204.30 | ops/s | 10x slower |
| simpleclientAdd | 6.05K | ± 81.49 | ops/s | 11x slower |
| openTelemetryInc | 1.42K | ± 200.34 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.36K | ± 141.76 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 34.74 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.18K | ± 21.54 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 102.33 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 97.20 | ops/s | 1.7x slower |
| openTelemetryClassic | 649.19 | ± 23.08 | ops/s | 8.0x slower |
| openTelemetryExponential | 569.41 | ± 11.85 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.07K | ± 6.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.45K | ± 19.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.78K | ± 4.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 508.13K | ± 7.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49456.989    ± 539.756  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1260.877     ± 34.736  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1421.191    ± 200.341  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1355.321    ± 141.758  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50422.776   ± 1616.112  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66135.978    ± 618.864  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57072.891    ± 254.875  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6054.104     ± 81.487  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6599.853    ± 165.847  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6346.423    ± 204.302  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        649.189     ± 23.080  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.414     ± 11.849  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5184.848     ± 21.538  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3033.110     ± 97.201  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4399.442    ± 102.333  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509783.549   ± 4870.902  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     508130.251   ± 7060.566  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513447.749  ± 19008.230  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527069.898   ± 6763.070  ops/s
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
