# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-27T05:31:07Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.90K | ± 1.92K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.33K | ± 992.65 | ops/s | 1.2x slower |
| prometheusAdd | 51.72K | ± 64.56 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.28K | ± 1.62K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 244.23 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.56K | ± 199.46 | ops/s | 9.9x slower |
| simpleclientAdd | 6.30K | ± 172.84 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 276.37 | ops/s | 44x slower |
| openTelemetryInc | 1.44K | ± 145.27 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.32K | ± 78.42 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.10K | ± 136.07 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 142.46 | ops/s | 1.1x slower |
| prometheusNative | 3.05K | ± 163.68 | ops/s | 1.7x slower |
| openTelemetryClassic | 660.93 | ± 17.01 | ops/s | 7.7x slower |
| openTelemetryExponential | 545.76 | ± 30.58 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.32K | ± 3.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 534.86K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.25K | ± 2.40K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 519.95K | ± 4.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49275.036   ± 1616.926  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1461.339    ± 276.368  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1436.388    ± 145.269  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1320.851     ± 78.416  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51717.607     ± 64.555  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64901.433   ± 1918.720  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56332.277    ± 992.649  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6300.426    ± 172.844  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6610.697    ± 244.231  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6562.535    ± 199.460  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.929     ± 17.010  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.763     ± 30.575  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5100.110    ± 136.067  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3050.630    ± 163.683  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4517.213    ± 142.455  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521248.088   ± 2398.570  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519952.893   ± 4420.689  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534860.244   ± 3077.953  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548316.553   ± 3831.909  ops/s
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
