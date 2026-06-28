# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-28T07:36:00Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.54K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.68K | ± 273.79 | ops/s | 1.2x slower |
| prometheusAdd | 51.02K | ± 676.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.53K | ± 1.43K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 7.75 | ops/s | 9.8x slower |
| simpleclientAdd | 6.49K | ± 17.45 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 196.94 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 220.22 | ops/s | 45x slower |
| openTelemetryInc | 1.43K | ± 76.30 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.35K | ± 148.41 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.22K | ± 299.84 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 31.67 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 77.97 | ops/s | 1.7x slower |
| openTelemetryClassic | 667.21 | ± 43.03 | ops/s | 7.8x slower |
| openTelemetryExponential | 543.25 | ± 35.73 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 542.47K | ± 5.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.97K | ± 9.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.93K | ± 4.59K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 506.70K | ± 5.96K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48529.458   ± 1425.044  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1443.959    ± 220.219  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1426.099     ± 76.296  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1350.275    ± 148.412  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51017.331    ± 676.272  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65543.177   ± 1679.706  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56676.589    ± 273.793  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6487.607     ± 17.452  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6701.761      ± 7.749  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6341.747    ± 196.942  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        667.213     ± 43.026  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.255     ± 35.726  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5219.684    ± 299.843  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3118.267     ± 77.968  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4389.220     ± 31.669  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506701.098   ± 5959.189  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510927.663   ± 4593.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531967.896   ± 9929.276  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542467.825   ± 5692.820  ops/s
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
