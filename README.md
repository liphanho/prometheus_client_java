# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-05T06:32:44Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.91K | ± 3.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 519.80 | ops/s | 1.1x slower |
| prometheusAdd | 51.42K | ± 209.67 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 45.17K | ± 7.87K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 189.77 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.49K | ± 181.00 | ops/s | 9.9x slower |
| simpleclientAdd | 6.31K | ± 280.30 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.32K | ± 107.69 | ops/s | 48x slower |
| openTelemetryInc | 1.30K | ± 141.36 | ops/s | 49x slower |
| openTelemetryAdd | 1.28K | ± 31.15 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 10.75 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 57.68 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 9.58 | ops/s | 1.7x slower |
| openTelemetryClassic | 690.07 | ± 15.90 | ops/s | 7.6x slower |
| openTelemetryExponential | 523.76 | ± 7.50 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 525.97K | ± 5.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 514.42K | ± 6.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.83K | ± 5.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 504.90K | ± 5.65K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45168.250   ± 7868.881  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1277.479     ± 31.155  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1304.405    ± 141.362  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1324.014    ± 107.694  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51417.250    ± 209.669  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63905.235   ± 3547.162  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56908.239    ± 519.800  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.993    ± 280.300  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6590.565    ± 189.775  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6486.810    ± 181.005  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.073     ± 15.899  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.759      ± 7.499  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5267.980     ± 10.745  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3125.346      ± 9.578  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4476.985     ± 57.684  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     504901.204   ± 5650.238  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509827.986   ± 5066.458  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     514424.815   ± 6537.097  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     525968.071   ± 5780.899  ops/s
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
