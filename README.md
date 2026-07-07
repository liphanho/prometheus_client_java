# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-07T07:25:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.22K | ± 1.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 87.20 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 92.72 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.24K | ± 822.50 | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 83.97 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.53K | ± 152.85 | ops/s | 9.8x slower |
| simpleclientAdd | 6.16K | ± 175.05 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 237.30 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.35K | ± 157.97 | ops/s | 48x slower |
| openTelemetryInc | 1.31K | ± 188.49 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 45.57 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 20.19 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 132.63 | ops/s | 1.7x slower |
| openTelemetryClassic | 662.61 | ± 10.02 | ops/s | 7.9x slower |
| openTelemetryExponential | 551.89 | ± 22.64 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.64K | ± 5.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.02K | ± 2.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.28K | ± 4.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 500.07K | ± 5.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48243.428    ± 822.502  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1560.562    ± 237.302  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.593    ± 188.491  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1349.315    ± 157.967  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51425.517     ± 92.719  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64216.256   ± 1216.707  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57045.623     ± 87.196  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6155.838    ± 175.048  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6595.601     ± 83.969  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6530.147    ± 152.848  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.611     ± 10.020  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.894     ± 22.639  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5259.760     ± 45.572  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.872    ± 132.628  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.507     ± 20.187  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500069.683   ± 5985.442  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507281.617   ± 4810.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525021.129   ± 2545.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530640.163   ± 5349.810  ops/s
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
