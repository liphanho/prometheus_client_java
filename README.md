# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-28T15:09:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.73K | ± 1.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.09K | ± 919.29 | ops/s | 1.2x slower |
| prometheusAdd | 48.79K | ± 2.86K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.61K | ± 1.10K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 14.34 | ops/s | 10.0x slower |
| simpleclientInc | 6.55K | ± 90.54 | ops/s | 10x slower |
| simpleclientAdd | 6.38K | ± 148.36 | ops/s | 10x slower |
| openTelemetryAdd | 1.70K | ± 100.88 | ops/s | 39x slower |
| openTelemetryInc | 1.32K | ± 40.80 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.32K | ± 155.60 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 261.61 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 8.29 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 51.00 | ops/s | 1.7x slower |
| openTelemetryClassic | 666.18 | ± 14.19 | ops/s | 8.0x slower |
| openTelemetryExponential | 530.78 | ± 15.44 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 513.93K | ± 8.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.85K | ± 3.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 498.36K | ± 5.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.86K | ± 5.95K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48608.014   ± 1104.844  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1700.815    ± 100.882  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1323.616     ± 40.795  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1315.190    ± 155.602  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48792.073   ± 2857.455  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65732.605   ± 1655.335  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56090.542    ± 919.289  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6384.053    ± 148.363  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.027     ± 90.537  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6597.496     ± 14.342  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        666.184     ± 14.191  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.780     ± 15.441  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5314.916    ± 261.611  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3115.999     ± 50.995  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.356      ± 8.290  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495861.983   ± 5952.923  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     498360.001   ± 5354.261  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503845.674   ± 3209.168  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513930.701   ± 8751.847  ops/s
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
