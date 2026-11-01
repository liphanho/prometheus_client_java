# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-01T10:05:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.57K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.87K | ± 319.38 | ops/s | 1.2x slower |
| prometheusAdd | 50.81K | ± 771.75 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.55K | ± 2.16K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 8.88 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.39K | ± 161.80 | ops/s | 10x slower |
| simpleclientAdd | 6.05K | ± 222.59 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 174.69 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.32K | ± 161.55 | ops/s | 50x slower |
| openTelemetryInc | 1.28K | ± 27.38 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 7.26 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 11.34 | ops/s | 1.2x slower |
| prometheusNative | 2.93K | ± 117.88 | ops/s | 1.8x slower |
| openTelemetryClassic | 707.91 | ± 13.33 | ops/s | 7.4x slower |
| openTelemetryExponential | 544.57 | ± 29.59 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 485.90K | ± 8.25K | ops/s | **fastest** |
| prometheusWriteToNull | 485.37K | ± 2.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.14K | ± 5.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.72K | ± 6.97K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48545.169   ± 2159.655  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1454.799    ± 174.688  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1280.850     ± 27.375  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1323.297    ± 161.548  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50811.194    ± 771.748  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65565.245   ± 1389.643  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56874.794    ± 319.377  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6053.381    ± 222.591  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.883      ± 8.884  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6389.506    ± 161.800  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.910     ± 13.332  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.573     ± 29.590  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5205.578      ± 7.259  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2932.123    ± 117.884  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4452.484     ± 11.341  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463716.258   ± 6966.396  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468136.738   ± 5679.671  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485903.089   ± 8245.128  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485366.672   ± 2479.732  ops/s
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
