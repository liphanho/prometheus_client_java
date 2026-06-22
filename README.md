# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-22T08:42:01Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.74K | ± 2.85K | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.93K | ± 2.39K | ops/s | 1.2x slower |
| prometheusAdd | 48.75K | ± 910.31 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.29K | ± 237.68 | ops/s | 1.3x slower |
| simpleclientInc | 6.30K | ± 36.87 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.27K | ± 29.82 | ops/s | 9.4x slower |
| simpleclientAdd | 6.08K | ± 179.64 | ops/s | 9.7x slower |
| openTelemetryIncNoLabels | 1.36K | ± 178.03 | ops/s | 43x slower |
| openTelemetryAdd | 1.33K | ± 73.48 | ops/s | 44x slower |
| openTelemetryInc | 1.26K | ± 48.53 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 213.85 | ops/s | **fastest** |
| prometheusClassic | 4.07K | ± 900.19 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 151.88 | ops/s | 1.5x slower |
| openTelemetryClassic | 583.53 | ± 13.74 | ops/s | 7.6x slower |
| openTelemetryExponential | 495.64 | ± 16.82 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 615.77K | ± 6.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.65K | ± 2.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 581.72K | ± 7.41K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 575.53K | ± 7.78K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44288.161    ± 237.679  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1330.439     ± 73.477  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.438     ± 48.531  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1364.575    ± 178.031  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48745.782    ± 910.308  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58738.835   ± 2845.019  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49932.450   ± 2387.691  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6083.419    ± 179.641  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6302.984     ± 36.870  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6271.124     ± 29.820  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        583.529     ± 13.735  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        495.641     ± 16.815  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4074.775    ± 900.193  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3005.387    ± 151.880  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.757    ± 213.845  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     575527.498   ± 7784.766  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     581716.783   ± 7413.782  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609652.723   ± 2544.325  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     615767.820   ± 6222.754  ops/s
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
