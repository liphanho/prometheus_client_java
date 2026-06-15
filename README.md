# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-15T08:38:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.56K | ± 412.45 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.94K | ± 1.95K | ops/s | 1.2x slower |
| prometheusAdd | 50.97K | ± 447.80 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.36K | ± 1.33K | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 160.77 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.58K | ± 13.94 | ops/s | 10.0x slower |
| simpleclientAdd | 6.31K | ± 167.08 | ops/s | 10x slower |
| openTelemetryAdd | 1.52K | ± 250.02 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 166.65 | ops/s | 50x slower |
| openTelemetryInc | 1.26K | ± 21.66 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 81.28 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 44.98 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 29.04 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.54 | ± 29.96 | ops/s | 7.6x slower |
| openTelemetryExponential | 556.39 | ± 36.23 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 528.65K | ± 4.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.37K | ± 8.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 511.82K | ± 3.51K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 501.92K | ± 6.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48360.221   ± 1334.479  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1524.857    ± 250.023  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.671     ± 21.660  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1322.299    ± 166.652  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50968.672    ± 447.802  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65562.903    ± 412.454  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55942.563   ± 1950.882  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6311.164    ± 167.081  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6595.582    ± 160.770  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6579.943     ± 13.935  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.544     ± 29.964  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.393     ± 36.227  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5286.336     ± 81.281  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3122.540     ± 29.038  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4400.901     ± 44.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501918.469   ± 6153.415  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     511815.418   ± 3510.740  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517374.398   ± 8964.605  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528645.525   ± 4376.211  ops/s
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
