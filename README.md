# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-02T05:31:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.10K | ± 314.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 265.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 199.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.42K | ± 1.11K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.70K | ± 13.62 | ops/s | 9.9x slower |
| simpleclientInc | 6.62K | ± 265.55 | ops/s | 10.0x slower |
| simpleclientAdd | 6.52K | ± 79.32 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.30K | ± 184.33 | ops/s | 51x slower |
| openTelemetryAdd | 1.27K | ± 38.14 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 67.51 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 428.37 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 37.43 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 164.12 | ops/s | 1.8x slower |
| openTelemetryClassic | 724.26 | ± 39.34 | ops/s | 7.4x slower |
| openTelemetryExponential | 551.10 | ± 24.52 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 513.59K | ± 5.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 504.85K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 497.53K | ± 4.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 493.00K | ± 3.46K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48424.906   ± 1111.114  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1267.242     ± 38.138  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1254.738     ± 67.513  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1300.582    ± 184.334  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51425.698    ± 199.766  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66100.262    ± 314.536  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56706.295    ± 265.042  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6515.750     ± 79.320  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6622.179    ± 265.545  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6700.699     ± 13.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        724.264     ± 39.335  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.096     ± 24.520  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5342.513    ± 428.371  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2947.993    ± 164.117  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4529.865     ± 37.431  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     493002.533   ± 3463.849  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     497527.105   ± 4714.905  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     504845.004   ± 4735.271  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513592.774   ± 5536.306  ops/s
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
