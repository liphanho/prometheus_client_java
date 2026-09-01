# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-01T08:38:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.13K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 111.43 | ops/s | 1.1x slower |
| prometheusAdd | 51.58K | ± 131.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.56K | ± 2.80K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 164.01 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.46K | ± 184.79 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 235.97 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 190.49 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.22K | ± 40.00 | ops/s | 53x slower |
| openTelemetryAdd | 1.20K | ± 53.36 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 417.25 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 65.94 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 135.99 | ops/s | 1.8x slower |
| openTelemetryClassic | 729.12 | ± 18.99 | ops/s | 7.2x slower |
| openTelemetryExponential | 541.13 | ± 7.86 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 517.57K | ± 1.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.07K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 499.61K | ± 3.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 490.67K | ± 9.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47563.869   ± 2802.018  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1201.854     ± 53.361  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1361.828    ± 190.486  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1220.101     ± 40.002  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51579.754    ± 131.659  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65126.966   ± 1393.008  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56968.434    ± 111.430  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6341.348    ± 235.966  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.781    ± 164.014  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6456.906    ± 184.788  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        729.123     ± 18.990  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.126      ± 7.857  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5260.846    ± 417.246  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2941.213    ± 135.990  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.184     ± 65.944  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     490670.343   ± 9438.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     499605.806   ± 3319.992  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513068.253   ± 5063.612  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     517565.411   ± 1810.560  ops/s
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
