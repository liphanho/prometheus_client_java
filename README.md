# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-15T06:08:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.25K | ± 541.51 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.20K | ± 374.36 | ops/s | 1.2x slower |
| prometheusAdd | 47.77K | ± 857.28 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.57K | ± 426.08 | ops/s | 1.4x slower |
| simpleclientInc | 6.32K | ± 30.10 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 5.95K | ± 276.93 | ops/s | 10.0x slower |
| simpleclientAdd | 5.95K | ± 178.47 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.47K | ± 55.97 | ops/s | 40x slower |
| openTelemetryInc | 1.32K | ± 82.63 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 121.48 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.64K | ± 948.97 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 50.64 | ops/s | 1.1x slower |
| prometheusNative | 3.08K | ± 78.69 | ops/s | 1.5x slower |
| openTelemetryClassic | 599.45 | ± 21.36 | ops/s | 7.7x slower |
| openTelemetryExponential | 503.22 | ± 8.19 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 624.63K | ± 5.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 599.56K | ± 17.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 594.30K | ± 5.42K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 583.77K | ± 5.71K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43565.482    ± 426.083  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1474.947     ± 55.969  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1324.366     ± 82.633  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1262.153    ± 121.476  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47767.231    ± 857.285  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59247.922    ± 541.508  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51204.992    ± 374.365  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5947.825    ± 178.468  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6319.596     ± 30.100  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5947.992    ± 276.927  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        599.454     ± 21.365  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        503.219      ± 8.191  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4642.266    ± 948.975  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3075.727     ± 78.690  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4379.314     ± 50.639  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     583766.919   ± 5714.391  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     594295.594   ± 5423.847  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     599556.911  ± 17781.750  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     624632.386   ± 5028.592  ops/s
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
