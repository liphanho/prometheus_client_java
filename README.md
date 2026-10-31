# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-31T09:19:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.69K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.17K | ± 1.46K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.95K | ± 1.60K | ops/s | 1.0x slower |
| prometheusAdd | 27.81K | ± 721.01 | ops/s | 1.1x slower |
| simpleclientInc | 6.33K | ± 75.09 | ops/s | 4.8x slower |
| simpleclientNoLabelsInc | 6.26K | ± 292.96 | ops/s | 4.9x slower |
| simpleclientAdd | 6.09K | ± 303.26 | ops/s | 5.0x slower |
| openTelemetryIncNoLabels | 1.33K | ± 103.26 | ops/s | 23x slower |
| openTelemetryAdd | 1.30K | ± 29.68 | ops/s | 24x slower |
| openTelemetryInc | 1.25K | ± 16.70 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.08K | ± 99.49 | ops/s | **fastest** |
| prometheusClassic | 3.07K | ± 190.86 | ops/s | 1.3x slower |
| prometheusNative | 2.08K | ± 260.46 | ops/s | 2.0x slower |
| openTelemetryClassic | 516.43 | ± 14.21 | ops/s | 7.9x slower |
| openTelemetryExponential | 419.60 | ± 20.49 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 329.99K | ± 2.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 327.68K | ± 3.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 311.53K | ± 1.76K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 308.24K | ± 1.89K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29947.871   ± 1603.554  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.447     ± 29.684  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.797     ± 16.701  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1326.930    ± 103.260  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27810.504    ± 721.015  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30691.856   ± 1255.298  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30169.993   ± 1456.173  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6090.870    ± 303.264  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6328.354     ± 75.091  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6259.518    ± 292.958  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        516.429     ± 14.209  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        419.598     ± 20.488  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3069.455    ± 190.862  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2082.415    ± 260.464  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4076.603     ± 99.494  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     308241.738   ± 1887.373  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     311527.468   ± 1756.450  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     327677.183   ± 3373.920  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     329990.097   ± 2304.890  ops/s
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
