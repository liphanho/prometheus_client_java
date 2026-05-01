# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-01T06:59:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.31K | ± 2.43K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.01K | ± 772.01 | ops/s | 1.1x slower |
| prometheusAdd | 48.66K | ± 697.72 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.55K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.28K | ± 47.27 | ops/s | 9.3x slower |
| simpleclientInc | 6.20K | ± 103.05 | ops/s | 9.4x slower |
| simpleclientAdd | 5.86K | ± 271.85 | ops/s | 9.9x slower |
| openTelemetryInc | 1.41K | ± 72.45 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.36K | ± 34.45 | ops/s | 43x slower |
| openTelemetryAdd | 1.35K | ± 5.79 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.89K | ± 969.32 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 54.61 | ops/s | 1.1x slower |
| prometheusNative | 3.12K | ± 47.07 | ops/s | 1.6x slower |
| openTelemetryClassic | 617.15 | ± 36.28 | ops/s | 7.9x slower |
| openTelemetryExponential | 518.67 | ± 7.21 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 639.30K | ± 2.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.85K | ± 3.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 601.18K | ± 2.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 596.32K | ± 3.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43553.176   ± 1327.265  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1349.701      ± 5.786  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1410.952     ± 72.446  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1360.076     ± 34.453  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48656.221    ± 697.722  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58310.790   ± 2432.399  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51013.393    ± 772.011  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5864.706    ± 271.846  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6196.547    ± 103.052  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6278.736     ± 47.271  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        617.145     ± 36.284  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.670      ± 7.209  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4893.022    ± 969.318  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3117.138     ± 47.070  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.068     ± 54.610  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     596323.346   ± 3675.604  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     601182.374   ± 2634.913  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630853.424   ± 3123.537  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     639296.407   ± 2885.526  ops/s
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
