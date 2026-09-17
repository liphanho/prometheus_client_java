# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T08:31:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.48K | ± 564.80 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.66K | ± 721.91 | ops/s | 1.2x slower |
| prometheusAdd | 48.08K | ± 264.72 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.07K | ± 1.10K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.26K | ± 32.01 | ops/s | 9.5x slower |
| simpleclientInc | 6.10K | ± 268.75 | ops/s | 9.8x slower |
| simpleclientAdd | 6.00K | ± 117.70 | ops/s | 9.9x slower |
| openTelemetryInc | 1.32K | ± 151.05 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.29K | ± 13.50 | ops/s | 46x slower |
| openTelemetryAdd | 1.25K | ± 52.68 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.91K | ± 927.10 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 31.18 | ops/s | 1.1x slower |
| prometheusNative | 3.14K | ± 122.74 | ops/s | 1.6x slower |
| openTelemetryClassic | 605.26 | ± 4.85 | ops/s | 8.1x slower |
| openTelemetryExponential | 509.48 | ± 12.90 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 619.12K | ± 9.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 611.19K | ± 3.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 592.01K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 580.86K | ± 4.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43069.083   ± 1102.882  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1253.316     ± 52.679  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.104    ± 151.046  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1289.722     ± 13.504  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48084.082    ± 264.720  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59482.012    ± 564.798  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51663.818    ± 721.910  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6003.045    ± 117.699  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6100.379    ± 268.745  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6262.097     ± 32.007  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.264      ± 4.845  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        509.476     ± 12.900  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4912.583    ± 927.100  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3138.178    ± 122.738  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4385.891     ± 31.177  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     580859.018   ± 4481.466  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     592011.448   ± 3091.181  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     611193.829   ± 3986.705  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     619115.222   ± 9135.644  ops/s
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
