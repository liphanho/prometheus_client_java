# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-14T05:25:32Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.77K | ± 975.45 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.81K | ± 864.59 | ops/s | 1.1x slower |
| prometheusAdd | 48.64K | ± 859.03 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.07K | ± 280.11 | ops/s | 1.3x slower |
| simpleclientInc | 6.28K | ± 41.36 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.06K | ± 269.81 | ops/s | 9.7x slower |
| simpleclientAdd | 6.05K | ± 206.29 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.35K | ± 91.18 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 113.07 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.28K | ± 8.33 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.62K | ± 910.23 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 43.10 | ops/s | 1.1x slower |
| prometheusNative | 3.15K | ± 40.73 | ops/s | 1.5x slower |
| openTelemetryClassic | 614.28 | ± 11.23 | ops/s | 7.5x slower |
| openTelemetryExponential | 507.62 | ± 19.64 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 644.33K | ± 5.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.54K | ± 4.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 607.37K | ± 2.93K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 583.97K | ± 8.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44070.161    ± 280.106  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1351.110     ± 91.181  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1306.188    ± 113.074  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1279.049      ± 8.329  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48636.343    ± 859.028  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58771.354    ± 975.453  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51808.601    ± 864.591  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6050.476    ± 206.294  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6283.814     ± 41.365  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6061.546    ± 269.814  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        614.281     ± 11.235  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        507.616     ± 19.638  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4621.636    ± 910.226  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3152.297     ± 40.729  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4395.123     ± 43.103  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     583968.830   ± 8195.318  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     607369.481   ± 2929.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630536.720   ± 4328.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     644333.406   ± 5265.139  ops/s
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
