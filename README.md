# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-13T10:18:41Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.26K | ± 445.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.18K | ± 462.62 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 57.32K | ± 3.45K | ops/s | 1.2x slower |
| prometheusAdd | 55.93K | ± 1.42K | ops/s | 1.2x slower |
| simpleclientInc | 10.57K | ± 140.05 | ops/s | 6.4x slower |
| simpleclientAdd | 10.36K | ± 430.29 | ops/s | 6.5x slower |
| simpleclientNoLabelsInc | 10.16K | ± 273.71 | ops/s | 6.6x slower |
| openTelemetryAdd | 2.04K | ± 234.52 | ops/s | 33x slower |
| openTelemetryInc | 2.03K | ± 271.53 | ops/s | 33x slower |
| openTelemetryIncNoLabels | 1.74K | ± 114.17 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.39K | ± 53.05 | ops/s | **fastest** |
| simpleclient | 6.97K | ± 100.03 | ops/s | 1.1x slower |
| prometheusNative | 5.02K | ± 350.80 | ops/s | 1.5x slower |
| openTelemetryClassic | 851.86 | ± 39.76 | ops/s | 8.7x slower |
| openTelemetryExponential | 710.44 | ± 62.62 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 785.67K | ± 51.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 745.69K | ± 46.61K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 711.58K | ± 39.57K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 692.36K | ± 8.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57320.588   ± 3448.160  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2040.231    ± 234.518  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2026.118    ± 271.529  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1743.918    ± 114.174  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      55932.970   ± 1420.595  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67262.143    ± 445.179  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65176.751    ± 462.623  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10357.881    ± 430.290  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10570.369    ± 140.055  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10163.020    ± 273.708  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        851.859     ± 39.761  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        710.435     ± 62.621  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7391.815     ± 53.049  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5024.945    ± 350.797  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6968.341    ± 100.027  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     711575.865  ± 39567.775  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     692355.741   ± 8301.309  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     745687.644  ± 46614.566  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     785670.342  ± 51419.123  ops/s
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
