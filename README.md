# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-07T09:30:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.01K | ± 33.11 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.75K | ± 929.67 | ops/s | 1.1x slower |
| prometheusAdd | 61.28K | ± 1.29K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.13K | ± 1.88K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 7.92K | ± 200.73 | ops/s | 9.6x slower |
| simpleclientInc | 7.91K | ± 158.96 | ops/s | 9.6x slower |
| simpleclientAdd | 7.62K | ± 221.04 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.70K | ± 123.12 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.68K | ± 46.68 | ops/s | 45x slower |
| openTelemetryInc | 1.56K | ± 88.61 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.67K | ± 7.47 | ops/s | **fastest** |
| simpleclient | 5.45K | ± 42.67 | ops/s | 1.0x slower |
| prometheusNative | 3.88K | ± 110.70 | ops/s | 1.5x slower |
| openTelemetryClassic | 749.51 | ± 41.11 | ops/s | 7.6x slower |
| openTelemetryExponential | 629.55 | ± 7.73 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 774.11K | ± 5.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 758.11K | ± 5.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 731.06K | ± 5.37K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 714.30K | ± 5.33K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56133.909   ± 1877.198  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1695.500    ± 123.115  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1561.993     ± 88.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1680.585     ± 46.679  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61280.343   ± 1293.640  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76006.813     ± 33.107  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66747.360    ± 929.671  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7618.718    ± 221.037  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7906.882    ± 158.960  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7921.448    ± 200.732  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.507     ± 41.107  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        629.551      ± 7.730  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5674.156      ± 7.472  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3877.645    ± 110.702  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5447.078     ± 42.671  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     714303.199   ± 5329.216  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     731059.441   ± 5366.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     758112.162   ± 5573.388  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     774105.000   ± 5166.668  ops/s
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
