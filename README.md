# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T06:59:01Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.14K | ± 918.02 | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 264.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.45K | ± 688.85 | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 63.18 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.62K | ± 9.26 | ops/s | 9.9x slower |
| simpleclientAdd | 6.49K | ± 10.92 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 190.23 | ops/s | 47x slower |
| openTelemetryInc | 1.29K | ± 10.49 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 50.38 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 36.77 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 63.28 | ops/s | 1.2x slower |
| prometheusNative | 2.91K | ± 126.77 | ops/s | 1.8x slower |
| openTelemetryClassic | 687.36 | ± 20.94 | ops/s | 7.6x slower |
| openTelemetryExponential | 550.75 | ± 42.63 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.50K | ± 7.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.45K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.73K | ± 6.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.07K | ± 7.21K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46454.128    ± 688.846  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1405.828    ± 190.226  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.343     ± 10.489  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1205.984     ± 50.376  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51580.981    ± 264.393  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65498.654   ± 1588.048  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56140.041    ± 918.018  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6492.525     ± 10.923  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.033     ± 63.175  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6615.412      ± 9.257  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.363     ± 20.939  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.750     ± 42.627  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5228.063     ± 36.774  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2914.518    ± 126.770  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4456.666     ± 63.275  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514730.846   ± 6310.036  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510065.253   ± 7213.628  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525445.820   ± 5266.370  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534501.859   ± 7562.941  ops/s
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
