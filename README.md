# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-07T09:42:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 74.62K | ± 2.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.05K | ± 1.01K | ops/s | 1.1x slower |
| prometheusAdd | 62.85K | ± 1.10K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.28K | ± 230.09 | ops/s | 1.3x slower |
| simpleclientInc | 7.97K | ± 30.79 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 7.77K | ± 289.61 | ops/s | 9.6x slower |
| simpleclientAdd | 7.52K | ± 240.25 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.86K | ± 132.78 | ops/s | 40x slower |
| openTelemetryAdd | 1.85K | ± 132.55 | ops/s | 40x slower |
| openTelemetryInc | 1.67K | ± 80.12 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.01K | ± 9.00 | ops/s | **fastest** |
| simpleclient | 5.75K | ± 104.78 | ops/s | 1.2x slower |
| prometheusNative | 3.99K | ± 119.60 | ops/s | 1.8x slower |
| openTelemetryClassic | 786.61 | ± 21.01 | ops/s | 8.9x slower |
| openTelemetryExponential | 670.42 | ± 11.33 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 752.16K | ± 6.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 733.87K | ± 12.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 686.16K | ± 8.00K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 674.80K | ± 12.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57283.231    ± 230.090  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1851.551    ± 132.547  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1667.134     ± 80.124  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1859.963    ± 132.781  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62854.532   ± 1104.615  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      74624.032   ± 2300.956  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66050.395   ± 1009.908  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7521.906    ± 240.254  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7971.295     ± 30.787  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7772.058    ± 289.612  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        786.611     ± 21.014  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        670.422     ± 11.334  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7013.246      ± 8.995  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3993.169    ± 119.598  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5751.477    ± 104.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     674795.537  ± 12342.497  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     686160.055   ± 7996.891  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     733867.060  ± 12239.797  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     752164.474   ± 6467.140  ops/s
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
