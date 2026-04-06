# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-06T06:02:15Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 441.68 | ops/s | 1.1x slower |
| prometheusAdd | 51.15K | ± 440.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.48K | ± 1.38K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.60K | ± 17.29 | ops/s | 9.9x slower |
| simpleclientInc | 6.58K | ± 196.60 | ops/s | 9.9x slower |
| simpleclientAdd | 6.37K | ± 196.16 | ops/s | 10x slower |
| openTelemetryAdd | 1.52K | ± 156.84 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.45K | ± 270.87 | ops/s | 45x slower |
| openTelemetryInc | 1.24K | ± 22.81 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 392.15 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 72.87 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 194.20 | ops/s | 1.8x slower |
| openTelemetryClassic | 718.04 | ± 27.94 | ops/s | 7.5x slower |
| openTelemetryExponential | 533.89 | ± 20.00 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.61K | ± 7.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 516.97K | ± 5.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 497.22K | ± 11.20K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 491.81K | ± 13.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48477.077   ± 1383.261  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1521.001    ± 156.842  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.146     ± 22.813  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1453.105    ± 270.867  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51146.887    ± 440.493  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65328.639   ± 1401.965  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56955.075    ± 441.680  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6368.108    ± 196.163  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6577.606    ± 196.599  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6598.684     ± 17.291  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.041     ± 27.944  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.894     ± 20.004  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5391.196    ± 392.155  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.744    ± 194.204  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4384.182     ± 72.871  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     491809.547  ± 13458.689  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     497221.911  ± 11202.706  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     516966.951   ± 5314.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533606.367   ± 7631.931  ops/s
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
