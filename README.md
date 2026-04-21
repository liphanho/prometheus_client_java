# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-21T06:05:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.01K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.06K | ± 581.52 | ops/s | 1.2x slower |
| prometheusAdd | 48.84K | ± 726.95 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.18K | ± 365.21 | ops/s | 1.4x slower |
| simpleclientInc | 6.22K | ± 136.35 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.03K | ± 213.48 | ops/s | 9.9x slower |
| simpleclientAdd | 5.83K | ± 227.29 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.46K | ± 67.33 | ops/s | 41x slower |
| openTelemetryAdd | 1.35K | ± 15.52 | ops/s | 44x slower |
| openTelemetryInc | 1.32K | ± 14.99 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 4.89 | ops/s | **fastest** |
| simpleclient | 4.61K | ± 87.12 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 95.85 | ops/s | 1.8x slower |
| openTelemetryClassic | 631.98 | ± 10.48 | ops/s | 8.7x slower |
| openTelemetryExponential | 513.32 | ± 17.10 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.33K | ± 3.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 627.37K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 604.25K | ± 6.57K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 598.88K | ± 8.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44180.316    ± 365.211  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1350.398     ± 15.516  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1323.712     ± 14.989  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1460.723     ± 67.334  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48836.045    ± 726.949  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60011.708   ± 1206.596  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52059.546    ± 581.525  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5827.794    ± 227.295  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6220.507    ± 136.348  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6033.114    ± 213.483  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        631.982     ± 10.483  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        513.323     ± 17.097  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5498.140      ± 4.887  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3122.889     ± 95.854  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4610.598     ± 87.125  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     598884.813   ± 8680.532  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     604245.356   ± 6570.529  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     627370.941   ± 3226.927  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643327.595   ± 3356.823  ops/s
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
