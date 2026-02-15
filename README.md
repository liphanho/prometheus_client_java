# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-15T05:40:09Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.75K | ± 183.60 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.49K | ± 1.43K | ops/s | 1.2x slower |
| prometheusAdd | 51.62K | ± 240.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.91K | ± 577.60 | ops/s | 1.3x slower |
| simpleclientInc | 6.78K | ± 31.45 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.52K | ± 147.64 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 326.22 | ops/s | 10x slower |
| openTelemetryAdd | 1.37K | ± 219.64 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 166.51 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 16.59 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 113.34 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 18.78 | ops/s | 1.2x slower |
| prometheusNative | 2.87K | ± 129.52 | ops/s | 1.8x slower |
| openTelemetryClassic | 695.18 | ± 44.09 | ops/s | 7.5x slower |
| openTelemetryExponential | 531.98 | ± 7.53 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.58K | ± 7.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.92K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.95K | ± 4.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.26K | ± 5.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49910.778    ± 577.595  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1369.504    ± 219.639  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1250.890     ± 16.594  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1307.689    ± 166.512  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51620.038    ± 240.494  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65748.810    ± 183.600  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56494.189   ± 1426.544  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6342.926    ± 326.218  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6782.696     ± 31.449  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6524.612    ± 147.642  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.176     ± 44.085  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.984      ± 7.528  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5247.153    ± 113.337  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2871.637    ± 129.523  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4523.677     ± 18.782  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509259.861   ± 5626.727  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514947.556   ± 4538.430  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531924.986   ± 6128.061  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536584.253   ± 7018.630  ops/s
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
