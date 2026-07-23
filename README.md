# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-23T06:42:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.10K | ± 985.15 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.05K | ± 2.06K | ops/s | 1.2x slower |
| prometheusAdd | 48.54K | ± 70.22 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.05K | ± 1.18K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.25K | ± 31.23 | ops/s | 9.6x slower |
| simpleclientInc | 6.08K | ± 110.63 | ops/s | 9.9x slower |
| simpleclientAdd | 6.06K | ± 190.03 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.45K | ± 178.31 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.41K | ± 83.12 | ops/s | 43x slower |
| openTelemetryInc | 1.29K | ± 62.88 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.33K | ± 466.63 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 46.62 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 55.52 | ops/s | 1.7x slower |
| openTelemetryClassic | 605.54 | ± 10.34 | ops/s | 8.8x slower |
| openTelemetryExponential | 497.39 | ± 6.62 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 638.45K | ± 3.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 632.83K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 614.97K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 593.23K | ± 6.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43048.839   ± 1182.974  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1451.017    ± 178.313  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.792     ± 62.878  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1406.460     ± 83.123  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48541.311     ± 70.222  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60095.733    ± 985.152  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50050.274   ± 2058.862  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6064.655    ± 190.028  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6075.704    ± 110.630  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6251.828     ± 31.227  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.540     ± 10.344  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        497.388      ± 6.623  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5327.068    ± 466.628  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3154.280     ± 55.516  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4534.992     ± 46.622  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     593226.693   ± 6515.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     614974.129   ± 3938.031  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     632828.031   ± 3647.693  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     638449.062   ± 3590.183  ops/s
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
