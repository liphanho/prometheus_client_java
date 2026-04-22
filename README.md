# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-22T06:03:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.22K | ± 1.40K | ops/s | **fastest** |
| prometheusAdd | 51.25K | ± 431.79 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 49.66K | ± 11.14K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.60K | ± 2.91K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 95.94 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.52K | ± 126.07 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 233.47 | ops/s | 10x slower |
| openTelemetryAdd | 1.62K | ± 294.84 | ops/s | 40x slower |
| openTelemetryInc | 1.44K | ± 222.74 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.27K | ± 207.16 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.46K | ± 220.21 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 39.83 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 138.86 | ops/s | 1.8x slower |
| openTelemetryClassic | 674.27 | ± 59.51 | ops/s | 8.1x slower |
| openTelemetryExponential | 553.99 | ± 38.68 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.64K | ± 6.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.27K | ± 2.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 527.92K | ± 4.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.27K | ± 3.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47596.703   ± 2914.670  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1620.160    ± 294.844  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1444.597    ± 222.741  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1269.164    ± 207.162  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51252.160    ± 431.787  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65217.384   ± 1404.294  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49661.592  ± 11141.925  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6327.842    ± 233.467  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.904     ± 95.943  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6518.147    ± 126.070  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.266     ± 59.508  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.987     ± 38.680  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5458.282    ± 220.212  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3079.126    ± 138.856  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4385.546     ± 39.835  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519270.943   ± 3538.110  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     527922.763   ± 4747.246  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533271.791   ± 2864.021  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540638.238   ± 6200.995  ops/s
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
