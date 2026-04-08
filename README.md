# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-08T05:54:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 54.81K | ± 6.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 961.61 | ops/s | 1.1x slower |
| prometheusAdd | 48.59K | ± 1.07K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 44.31K | ± 125.05 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 6.26K | ± 29.86 | ops/s | 8.8x slower |
| simpleclientInc | 6.15K | ± 157.45 | ops/s | 8.9x slower |
| simpleclientAdd | 6.03K | ± 171.39 | ops/s | 9.1x slower |
| openTelemetryInc | 1.45K | ± 121.52 | ops/s | 38x slower |
| openTelemetryAdd | 1.40K | ± 39.60 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.33K | ± 59.58 | ops/s | 41x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.59K | ± 54.42 | ops/s | **fastest** |
| prometheusClassic | 4.38K | ± 12.34 | ops/s | 1.0x slower |
| prometheusNative | 2.94K | ± 81.95 | ops/s | 1.6x slower |
| openTelemetryClassic | 597.58 | ± 6.68 | ops/s | 7.7x slower |
| openTelemetryExponential | 490.72 | ± 9.78 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 617.69K | ± 9.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 608.45K | ± 5.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 591.45K | ± 2.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 574.99K | ± 5.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44313.138    ± 125.050  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1402.959     ± 39.597  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1454.578    ± 121.516  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1326.188     ± 59.576  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48585.840   ± 1066.248  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      54806.551   ± 6809.841  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51555.857    ± 961.611  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6027.449    ± 171.389  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6150.310    ± 157.447  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6257.924     ± 29.862  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        597.576      ± 6.681  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        490.719      ± 9.784  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4384.218     ± 12.338  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2942.204     ± 81.952  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4592.327     ± 54.424  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     574991.618   ± 5161.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     591445.077   ± 2448.376  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     608448.218   ± 5124.582  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     617689.806   ± 9751.953  ops/s
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
