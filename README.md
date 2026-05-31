# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-31T07:36:29Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.47K | ± 4.09K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.70K | ± 708.49 | ops/s | 1.1x slower |
| prometheusAdd | 45.83K | ± 3.76K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.41K | ± 220.42 | ops/s | 1.3x slower |
| simpleclientInc | 6.26K | ± 150.29 | ops/s | 9.0x slower |
| simpleclientNoLabelsInc | 6.25K | ± 31.15 | ops/s | 9.0x slower |
| simpleclientAdd | 5.87K | ± 258.70 | ops/s | 9.6x slower |
| openTelemetryInc | 1.39K | ± 75.69 | ops/s | 41x slower |
| openTelemetryAdd | 1.28K | ± 6.85 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.27K | ± 90.95 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.23K | ± 55.23 | ops/s | **fastest** |
| prometheusClassic | 4.10K | ± 886.49 | ops/s | 1.0x slower |
| prometheusNative | 3.02K | ± 92.65 | ops/s | 1.4x slower |
| openTelemetryClassic | 619.65 | ± 0.97 | ops/s | 6.8x slower |
| openTelemetryExponential | 529.54 | ± 1.33 | ops/s | 8.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 613.36K | ± 3.04K | ops/s | **fastest** |
| prometheusWriteToByteArray | 603.77K | ± 6.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 579.07K | ± 5.35K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 574.13K | ± 3.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44413.314    ± 220.420  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1279.137      ± 6.852  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.257     ± 75.693  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1268.508     ± 90.953  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      45833.710   ± 3759.133  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56473.273   ± 4091.704  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51703.860    ± 708.494  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5866.083    ± 258.704  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6260.251    ± 150.293  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6248.168     ± 31.148  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        619.647      ± 0.972  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.541      ± 1.328  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4096.033    ± 886.491  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3016.884     ± 92.649  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4231.249     ± 55.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     574127.189   ± 3847.455  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     579066.659   ± 5351.390  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     603771.431   ± 6123.252  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     613364.743   ± 3040.982  ops/s
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
