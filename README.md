# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-11T09:38:37Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.00K | ± 4.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.64K | ± 348.03 | ops/s | 1.1x slower |
| prometheusAdd | 48.37K | ± 3.69K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.31K | ± 1.53K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 60.98 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.48K | ± 204.86 | ops/s | 9.9x slower |
| simpleclientAdd | 6.19K | ± 264.20 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 246.75 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.39K | ± 152.29 | ops/s | 46x slower |
| openTelemetryInc | 1.37K | ± 200.97 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 116.04 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 31.91 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 32.67 | ops/s | 1.8x slower |
| openTelemetryClassic | 683.44 | ± 38.14 | ops/s | 8.1x slower |
| openTelemetryExponential | 561.63 | ± 19.89 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.04K | ± 5.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.79K | ± 3.00K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.46K | ± 3.17K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 497.34K | ± 6.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48310.429   ± 1526.691  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1428.391    ± 246.753  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.065    ± 200.970  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1392.350    ± 152.285  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48369.334   ± 3693.869  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63999.930   ± 4221.529  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56644.133    ± 348.031  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.888    ± 264.201  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6646.992     ± 60.977  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.271    ± 204.856  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.442     ± 38.144  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.633     ± 19.894  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5553.589    ± 116.040  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3168.534     ± 32.672  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4487.722     ± 31.913  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497344.892   ± 6223.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516461.045   ± 3169.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521789.947   ± 3004.834  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533035.744   ± 5752.669  ops/s
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
