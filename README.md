# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-03T07:10:41Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.11K | ± 3.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 601.79 | ops/s | 1.1x slower |
| prometheusAdd | 48.97K | ± 650.11 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 44.37K | ± 454.27 | ops/s | 1.3x slower |
| simpleclientAdd | 6.16K | ± 34.89 | ops/s | 9.1x slower |
| simpleclientInc | 6.15K | ± 155.31 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 5.87K | ± 346.12 | ops/s | 9.6x slower |
| openTelemetryAdd | 1.38K | ± 81.77 | ops/s | 41x slower |
| openTelemetryInc | 1.33K | ± 172.92 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.30K | ± 57.15 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 44.17 | ops/s | **fastest** |
| prometheusClassic | 4.40K | ± 9.75 | ops/s | 1.0x slower |
| prometheusNative | 3.16K | ± 47.22 | ops/s | 1.4x slower |
| openTelemetryClassic | 590.63 | ± 12.15 | ops/s | 7.7x slower |
| openTelemetryExponential | 497.22 | ± 1.98 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 615.02K | ± 6.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 607.22K | ± 5.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 589.67K | ± 2.04K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 573.71K | ± 7.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44367.606    ± 454.267  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1383.649     ± 81.772  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1333.736    ± 172.917  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1300.458     ± 57.154  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48970.092    ± 650.109  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56113.227   ± 3082.033  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51189.514    ± 601.794  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6163.544     ± 34.890  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6146.978    ± 155.306  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5872.884    ± 346.122  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        590.628     ± 12.148  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        497.217      ± 1.984  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4395.423      ± 9.752  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3158.028     ± 47.222  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4566.836     ± 44.166  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     573708.900   ± 7440.986  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     589673.876   ± 2036.992  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     607219.471   ± 5076.826  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     615019.362   ± 6173.427  ops/s
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
