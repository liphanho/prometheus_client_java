# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-01T05:46:46Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.61K | ± 455.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.64K | ± 722.93 | ops/s | 1.2x slower |
| prometheusAdd | 48.33K | ± 334.53 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.06K | ± 1.78K | ops/s | 1.4x slower |
| simpleclientInc | 6.24K | ± 113.51 | ops/s | 9.6x slower |
| simpleclientAdd | 5.98K | ± 84.88 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 5.82K | ± 77.13 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 136.26 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.35K | ± 35.77 | ops/s | 44x slower |
| openTelemetryAdd | 1.32K | ± 12.37 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.47K | ± 761.22 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 21.27 | ops/s | 1.0x slower |
| prometheusNative | 3.17K | ± 33.33 | ops/s | 1.4x slower |
| openTelemetryClassic | 590.74 | ± 7.52 | ops/s | 7.6x slower |
| openTelemetryExponential | 523.18 | ± 6.62 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 644.44K | ± 3.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 627.91K | ± 4.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 607.08K | ± 2.99K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 599.63K | ± 5.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43058.758   ± 1776.528  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1316.079     ± 12.374  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1397.719    ± 136.264  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1346.953     ± 35.772  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48330.669    ± 334.526  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59613.587    ± 455.160  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51641.898    ± 722.931  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5983.646     ± 84.884  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6236.143    ± 113.510  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5819.637     ± 77.131  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        590.739      ± 7.521  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.185      ± 6.616  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4474.380    ± 761.219  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3169.894     ± 33.331  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4399.344     ± 21.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     599631.778   ± 5218.585  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     607083.218   ± 2988.300  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     627907.216   ± 4438.276  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     644441.615   ± 3319.835  ops/s
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
