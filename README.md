# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-26T11:47:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.09K | ± 604.81 | ops/s | **fastest** |
| prometheusNoLabelsInc | 61.99K | ± 575.22 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 58.88K | ± 709.17 | ops/s | 1.1x slower |
| prometheusAdd | 53.19K | ± 769.87 | ops/s | 1.2x slower |
| simpleclientInc | 10.21K | ± 113.20 | ops/s | 6.3x slower |
| simpleclientNoLabelsInc | 10.03K | ± 214.54 | ops/s | 6.4x slower |
| simpleclientAdd | 9.69K | ± 490.46 | ops/s | 6.6x slower |
| openTelemetryAdd | 2.03K | ± 228.98 | ops/s | 31x slower |
| openTelemetryIncNoLabels | 1.77K | ± 220.19 | ops/s | 36x slower |
| openTelemetryInc | 1.71K | ± 21.38 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.64K | ± 125.73 | ops/s | **fastest** |
| simpleclient | 6.32K | ± 102.63 | ops/s | 1.1x slower |
| prometheusNative | 4.27K | ± 79.29 | ops/s | 1.6x slower |
| openTelemetryClassic | 837.66 | ± 25.22 | ops/s | 7.9x slower |
| openTelemetryExponential | 659.39 | ± 27.33 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 742.71K | ± 63.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 738.77K | ± 51.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 699.69K | ± 15.84K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 652.53K | ± 27.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      58880.726    ± 709.174  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2034.635    ± 228.975  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1713.993     ± 21.379  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1766.940    ± 220.191  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      53190.640    ± 769.875  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64090.830    ± 604.812  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      61985.418    ± 575.223  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9691.213    ± 490.465  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10209.191    ± 113.197  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10026.211    ± 214.544  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        837.657     ± 25.225  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        659.393     ± 27.328  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6641.128    ± 125.728  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4268.999     ± 79.293  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6319.579    ± 102.633  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     699690.838  ± 15837.763  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     652525.544  ± 27508.642  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     738769.744  ± 51605.831  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     742707.345  ± 63436.942  ops/s
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
