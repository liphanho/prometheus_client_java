# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-13T07:06:19Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.75K | ± 162.80 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.34K | ± 3.02K | ops/s | 1.2x slower |
| prometheusAdd | 48.27K | ± 447.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 45.10K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.21K | ± 107.84 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.13K | ± 196.73 | ops/s | 9.7x slower |
| simpleclientAdd | 5.78K | ± 240.06 | ops/s | 10x slower |
| openTelemetryInc | 1.44K | ± 183.62 | ops/s | 42x slower |
| openTelemetryAdd | 1.33K | ± 106.94 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 80.51 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.56K | ± 50.20 | ops/s | **fastest** |
| prometheusClassic | 4.48K | ± 720.88 | ops/s | 1.0x slower |
| prometheusNative | 3.10K | ± 148.16 | ops/s | 1.5x slower |
| openTelemetryClassic | 628.57 | ± 30.91 | ops/s | 7.3x slower |
| openTelemetryExponential | 504.99 | ± 14.06 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 638.57K | ± 4.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.06K | ± 7.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 605.93K | ± 5.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 596.61K | ± 3.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45096.102   ± 1282.541  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1327.293    ± 106.942  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1435.679    ± 183.619  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.603     ± 80.512  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48266.787    ± 447.328  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59747.252    ± 162.796  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50338.890   ± 3022.238  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5783.720    ± 240.055  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6210.150    ± 107.842  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6133.439    ± 196.735  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        628.568     ± 30.915  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        504.995     ± 14.058  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4477.851    ± 720.878  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3095.178    ± 148.160  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4563.891     ± 50.204  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     596609.498   ± 3049.044  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     605926.480   ± 5439.773  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630059.597   ± 7876.019  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     638570.467   ± 4089.609  ops/s
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
