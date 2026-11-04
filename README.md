# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-04T09:58:47Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.11K | ± 1.27K | ops/s | **fastest** |
| prometheusNoLabelsInc | 62.71K | ± 329.04 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 61.86K | ± 2.67K | ops/s | 1.0x slower |
| prometheusAdd | 53.75K | ± 468.35 | ops/s | 1.2x slower |
| simpleclientInc | 10.05K | ± 193.32 | ops/s | 6.3x slower |
| simpleclientAdd | 9.97K | ± 164.44 | ops/s | 6.3x slower |
| simpleclientNoLabelsInc | 9.75K | ± 288.17 | ops/s | 6.5x slower |
| openTelemetryAdd | 1.88K | ± 207.64 | ops/s | 34x slower |
| openTelemetryIncNoLabels | 1.86K | ± 239.62 | ops/s | 34x slower |
| openTelemetryInc | 1.77K | ± 11.27 | ops/s | 36x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.16K | ± 110.06 | ops/s | **fastest** |
| simpleclient | 6.74K | ± 114.29 | ops/s | 1.1x slower |
| prometheusNative | 4.51K | ± 57.82 | ops/s | 1.6x slower |
| openTelemetryClassic | 799.05 | ± 11.66 | ops/s | 9.0x slower |
| openTelemetryExponential | 703.41 | ± 33.71 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 776.81K | ± 39.27K | ops/s | **fastest** |
| prometheusWriteToNull | 759.03K | ± 40.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 723.32K | ± 57.58K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 705.06K | ± 27.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61864.909   ± 2673.797  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1876.231    ± 207.643  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1768.964     ± 11.268  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1858.612    ± 239.615  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      53748.020    ± 468.349  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63112.316   ± 1273.533  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      62713.628    ± 329.045  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9965.442    ± 164.442  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10048.650    ± 193.325  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9752.812    ± 288.169  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        799.047     ± 11.663  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        703.408     ± 33.706  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7164.529    ± 110.063  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4514.884     ± 57.818  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6742.301    ± 114.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     705057.279  ± 27159.512  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     723323.115  ± 57584.884  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     776812.301  ± 39271.011  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     759030.289  ± 40141.477  ops/s
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
