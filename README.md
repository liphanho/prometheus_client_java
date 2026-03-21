# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-21T05:23:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.49K | ± 708.31 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.05K | ± 853.26 | ops/s | 1.2x slower |
| prometheusAdd | 50.99K | ± 663.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.01K | ± 1.95K | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 15.20 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 186.15 | ops/s | 10x slower |
| simpleclientAdd | 6.09K | ± 16.57 | ops/s | 11x slower |
| openTelemetryAdd | 1.66K | ± 52.25 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.29K | ± 124.27 | ops/s | 52x slower |
| openTelemetryInc | 1.27K | ± 25.70 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 77.30 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 72.05 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 135.15 | ops/s | 1.7x slower |
| openTelemetryClassic | 702.33 | ± 18.55 | ops/s | 7.5x slower |
| openTelemetryExponential | 550.42 | ± 16.48 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 552.52K | ± 10.00K | ops/s | **fastest** |
| prometheusWriteToNull | 543.83K | ± 2.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.11K | ± 2.51K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 516.58K | ± 4.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50010.605   ± 1947.014  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1660.275     ± 52.248  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1274.984     ± 25.697  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1289.131    ± 124.266  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50989.026    ± 663.282  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66488.006    ± 708.310  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56045.961    ± 853.260  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6087.670     ± 16.566  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6768.764     ± 15.201  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6477.241    ± 186.154  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.333     ± 18.555  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.425     ± 16.478  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5281.469     ± 77.298  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3039.172    ± 135.146  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4536.589     ± 72.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516582.861   ± 4604.098  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519105.721   ± 2513.784  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     552521.503  ± 10001.999  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     543832.971   ± 2785.865  ops/s
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
