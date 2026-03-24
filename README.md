# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-24T05:37:47Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.43K | ± 211.57 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 1.14K | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 137.30 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.86K | ± 545.46 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.69K | ± 19.63 | ops/s | 9.9x slower |
| simpleclientInc | 6.59K | ± 161.24 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 207.36 | ops/s | 11x slower |
| openTelemetryAdd | 1.58K | ± 166.96 | ops/s | 42x slower |
| openTelemetryInc | 1.55K | ± 109.46 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.40K | ± 158.94 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 390.51 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 15.06 | ops/s | 1.2x slower |
| prometheusNative | 2.89K | ± 102.35 | ops/s | 1.9x slower |
| openTelemetryClassic | 673.36 | ± 35.33 | ops/s | 8.1x slower |
| openTelemetryExponential | 534.39 | ± 20.47 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 548.88K | ± 7.73K | ops/s | **fastest** |
| prometheusWriteToNull | 541.92K | ± 6.03K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.68K | ± 2.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.33K | ± 9.02K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49861.633    ± 545.463  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1575.243    ± 166.958  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1554.455    ± 109.457  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1395.377    ± 158.940  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51357.240    ± 137.297  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66433.332    ± 211.566  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56588.902   ± 1144.163  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6297.849    ± 207.355  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6592.777    ± 161.243  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6690.584     ± 19.627  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.356     ± 35.331  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.389     ± 20.472  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5485.543    ± 390.507  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2892.809    ± 102.349  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.706     ± 15.061  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524675.734   ± 2240.330  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518334.860   ± 9024.589  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548881.531   ± 7730.763  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541915.467   ± 6028.989  ops/s
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
