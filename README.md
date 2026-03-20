# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-20T05:31:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.66K | ± 11.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.79K | ± 321.95 | ops/s | 1.0x slower |
| prometheusAdd | 51.67K | ± 171.78 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 48.36K | ± 928.04 | ops/s | 1.2x slower |
| simpleclientInc | 6.72K | ± 126.90 | ops/s | 8.7x slower |
| simpleclientNoLabelsInc | 6.51K | ± 260.60 | ops/s | 9.0x slower |
| simpleclientAdd | 6.44K | ± 193.73 | ops/s | 9.1x slower |
| openTelemetryAdd | 1.37K | ± 238.38 | ops/s | 43x slower |
| openTelemetryInc | 1.26K | ± 34.77 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.21K | ± 27.19 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 71.59 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 32.21 | ops/s | 1.1x slower |
| prometheusNative | 3.05K | ± 147.04 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.00 | ± 45.44 | ops/s | 7.5x slower |
| openTelemetryExponential | 523.73 | ± 13.14 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.08K | ± 2.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.02K | ± 5.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.91K | ± 6.04K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.20K | ± 4.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48364.927    ± 928.036  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1371.684    ± 238.382  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1262.022     ± 34.767  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1209.877     ± 27.186  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51674.337    ± 171.785  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58664.059  ± 11149.433  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56786.879    ± 321.950  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6440.842    ± 193.732  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6720.076    ± 126.898  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6507.092    ± 260.599  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.997     ± 45.439  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.732     ± 13.143  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5204.842     ± 71.588  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3054.637    ± 147.041  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4555.224     ± 32.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509203.538   ± 4317.753  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514906.849   ± 6044.859  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526017.493   ± 5845.949  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529080.489   ± 2538.971  ops/s
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
