# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-18T05:42:12Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.61K | ± 1.62K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.16K | ± 509.69 | ops/s | 1.1x slower |
| prometheusAdd | 51.23K | ± 714.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.53K | ± 2.01K | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 166.39 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.57K | ± 181.15 | ops/s | 10.0x slower |
| simpleclientAdd | 6.25K | ± 255.41 | ops/s | 11x slower |
| openTelemetryAdd | 1.57K | ± 210.51 | ops/s | 42x slower |
| openTelemetryInc | 1.44K | ± 138.97 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.34K | ± 147.64 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 8.57 | ops/s | **fastest** |
| simpleclient | 4.57K | ± 47.41 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 152.30 | ops/s | 1.7x slower |
| openTelemetryClassic | 710.73 | ± 37.71 | ops/s | 7.4x slower |
| openTelemetryExponential | 565.49 | ± 8.55 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.24K | ± 10.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 516.41K | ± 8.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.01K | ± 6.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 505.50K | ± 4.97K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49528.668   ± 2006.595  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1568.993    ± 210.514  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1439.784    ± 138.972  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1337.720    ± 147.638  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51234.479    ± 714.657  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65606.989   ± 1617.601  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57159.035    ± 509.692  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6246.836    ± 255.415  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6639.475    ± 166.392  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6573.415    ± 181.151  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.731     ± 37.713  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.490      ± 8.550  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5262.519      ± 8.571  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3052.651    ± 152.297  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4573.182     ± 47.411  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507013.074   ± 6118.519  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505496.044   ± 4967.314  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     516408.896   ± 8235.982  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529239.405  ± 10703.913  ops/s
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
