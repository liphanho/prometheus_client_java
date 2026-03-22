# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-22T05:38:08Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.26K | ± 225.88 | ops/s | **fastest** |
| prometheusInc | 30.73K | ± 687.02 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.87K | ± 870.03 | ops/s | 1.0x slower |
| prometheusAdd | 27.86K | ± 900.77 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.05K | ± 90.16 | ops/s | 4.4x slower |
| simpleclientInc | 6.96K | ± 66.60 | ops/s | 4.5x slower |
| simpleclientAdd | 6.83K | ± 42.39 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.41K | ± 82.44 | ops/s | 22x slower |
| openTelemetryInc | 1.26K | ± 11.79 | ops/s | 25x slower |
| openTelemetryAdd | 1.24K | ± 91.38 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.56K | ± 88.02 | ops/s | **fastest** |
| prometheusClassic | 3.20K | ± 199.03 | ops/s | 1.4x slower |
| prometheusNative | 2.19K | ± 239.00 | ops/s | 2.1x slower |
| openTelemetryClassic | 482.14 | ± 40.14 | ops/s | 9.5x slower |
| openTelemetryExponential | 387.45 | ± 9.71 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 335.50K | ± 1.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 333.84K | ± 1.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 307.15K | ± 1.50K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 305.59K | ± 1.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29872.241    ± 870.031  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1241.341     ± 91.384  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.639     ± 11.789  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1413.141     ± 82.436  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27858.237    ± 900.772  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30731.907    ± 687.018  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31263.547    ± 225.878  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6826.989     ± 42.392  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6956.029     ± 66.605  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7049.586     ± 90.157  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        482.142     ± 40.142  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        387.454      ± 9.707  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3203.297    ± 199.026  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2185.034    ± 238.999  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4559.827     ± 88.021  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     305585.311   ± 1047.431  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     307151.689   ± 1498.559  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     333844.809   ± 1424.441  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     335496.816   ± 1368.479  ops/s
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
