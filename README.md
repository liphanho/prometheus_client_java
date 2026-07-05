# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-05T07:22:10Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 106.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 703.53 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 219.87 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.45K | ± 991.75 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 9.97 | ops/s | 10.0x slower |
| simpleclientInc | 6.59K | ± 164.19 | ops/s | 10.0x slower |
| simpleclientAdd | 6.16K | ± 311.63 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.29K | ± 133.79 | ops/s | 51x slower |
| openTelemetryAdd | 1.28K | ± 33.94 | ops/s | 52x slower |
| openTelemetryInc | 1.23K | ± 84.24 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 264.24 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 127.54 | ops/s | 1.2x slower |
| prometheusNative | 3.20K | ± 12.30 | ops/s | 1.7x slower |
| openTelemetryClassic | 675.99 | ± 34.63 | ops/s | 7.9x slower |
| openTelemetryExponential | 580.21 | ± 23.25 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.51K | ± 3.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.99K | ± 4.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.32K | ± 3.56K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 505.86K | ± 4.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49451.262    ± 991.750  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.244     ± 33.943  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1234.704     ± 84.242  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1289.556    ± 133.794  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51047.598    ± 219.865  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65821.993    ± 106.230  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56645.323    ± 703.533  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6155.469    ± 311.629  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.786    ± 164.186  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6607.195      ± 9.973  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.993     ± 34.628  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.214     ± 23.252  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5311.988    ± 264.242  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3195.890     ± 12.296  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.116    ± 127.537  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505863.894   ± 4990.693  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510322.479   ± 3558.823  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528987.658   ± 4349.918  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538513.274   ± 3508.073  ops/s
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
