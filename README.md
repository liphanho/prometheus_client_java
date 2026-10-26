# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-26T08:45:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.06K | ± 1.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.23K | ± 135.77 | ops/s | 1.1x slower |
| prometheusAdd | 51.46K | ± 211.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.38K | ± 1.41K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 166.24 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.51K | ± 134.38 | ops/s | 10.0x slower |
| simpleclientAdd | 6.31K | ± 278.48 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 245.22 | ops/s | 45x slower |
| openTelemetryInc | 1.38K | ± 219.08 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.25K | ± 10.59 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.56K | ± 283.50 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 50.42 | ops/s | 1.3x slower |
| prometheusNative | 3.10K | ± 136.98 | ops/s | 1.8x slower |
| openTelemetryClassic | 663.11 | ± 26.72 | ops/s | 8.4x slower |
| openTelemetryExponential | 596.43 | ± 35.74 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 528.76K | ± 2.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.89K | ± 5.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.53K | ± 4.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.93K | ± 2.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48375.270   ± 1412.504  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1431.401    ± 245.220  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1381.657    ± 219.077  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1252.739     ± 10.593  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51459.447    ± 211.396  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65060.178   ± 1137.898  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57228.688    ± 135.773  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6310.447    ± 278.478  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6584.148    ± 166.241  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6512.298    ± 134.379  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.111     ± 26.720  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        596.428     ± 35.740  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5563.335    ± 283.503  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3097.225    ± 136.985  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.212     ± 50.424  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499928.522   ± 2984.826  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507530.831   ± 4665.125  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525888.126   ± 5622.662  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528763.477   ± 2785.239  ops/s
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
