# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-04T05:26:14Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.43K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.19K | ± 256.83 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 152.11 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.36K | ± 876.20 | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 130.47 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.55K | ± 191.01 | ops/s | 10.0x slower |
| simpleclientAdd | 6.21K | ± 30.91 | ops/s | 11x slower |
| openTelemetryInc | 1.39K | ± 180.09 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.29K | ± 77.11 | ops/s | 51x slower |
| openTelemetryAdd | 1.26K | ± 62.56 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 72.88 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 36.95 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 217.15 | ops/s | 1.7x slower |
| openTelemetryClassic | 664.44 | ± 21.00 | ops/s | 7.9x slower |
| openTelemetryExponential | 577.92 | ± 32.53 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.97K | ± 6.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.93K | ± 4.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.72K | ± 2.53K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 514.07K | ± 2.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50362.207    ± 876.205  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.270     ± 62.564  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1385.993    ± 180.092  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1290.484     ± 77.112  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51433.604    ± 152.108  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65432.287   ± 1324.096  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57190.458    ± 256.831  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6207.516     ± 30.911  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6697.913    ± 130.467  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6553.909    ± 191.005  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        664.445     ± 21.000  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        577.917     ± 32.533  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5262.735     ± 72.881  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3132.942    ± 217.148  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.743     ± 36.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514065.653   ± 2736.510  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514724.510   ± 2530.006  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531933.655   ± 4272.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540972.027   ± 5999.611  ops/s
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
