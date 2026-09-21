# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-21T08:58:27Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.67K | ± 625.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 428.27 | ops/s | 1.2x slower |
| prometheusAdd | 51.00K | ± 775.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.14K | ± 922.53 | ops/s | 1.4x slower |
| simpleclientInc | 6.51K | ± 189.08 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 177.28 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 269.87 | ops/s | 11x slower |
| openTelemetryAdd | 1.56K | ± 81.15 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.28K | ± 139.93 | ops/s | 51x slower |
| openTelemetryInc | 1.21K | ± 84.90 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 267.18 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 59.29 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 107.47 | ops/s | 1.7x slower |
| openTelemetryClassic | 652.80 | ± 21.50 | ops/s | 8.0x slower |
| openTelemetryExponential | 536.87 | ± 25.73 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.73K | ± 3.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 532.56K | ± 2.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 523.89K | ± 6.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.08K | ± 6.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48143.377    ± 922.533  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1564.780     ± 81.149  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1211.565     ± 84.901  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1275.641    ± 139.929  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50999.377    ± 775.375  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65669.269    ± 625.941  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56653.804    ± 428.271  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6142.776    ± 269.874  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6512.037    ± 189.079  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6396.406    ± 177.279  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.795     ± 21.496  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.872     ± 25.727  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5236.016    ± 267.177  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3154.102    ± 107.475  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4359.262     ± 59.294  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515078.177   ± 6186.984  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     523887.095   ± 6552.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     532564.929   ± 2264.141  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535730.815   ± 3079.779  ops/s
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
