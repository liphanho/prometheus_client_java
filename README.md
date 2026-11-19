# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-19T11:13:12Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.77K | ± 197.77 | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.78K | ± 737.02 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 66.41K | ± 3.29K | ops/s | 1.1x slower |
| prometheusAdd | 59.61K | ± 1.93K | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 11.00K | ± 171.04 | ops/s | 6.3x slower |
| simpleclientInc | 10.86K | ± 170.20 | ops/s | 6.4x slower |
| simpleclientAdd | 10.72K | ± 111.06 | ops/s | 6.5x slower |
| openTelemetryIncNoLabels | 1.92K | ± 374.41 | ops/s | 36x slower |
| openTelemetryAdd | 1.88K | ± 256.09 | ops/s | 37x slower |
| openTelemetryInc | 1.80K | ± 206.90 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.17K | ± 99.94 | ops/s | **fastest** |
| simpleclient | 6.76K | ± 377.64 | ops/s | 1.1x slower |
| prometheusNative | 5.02K | ± 387.29 | ops/s | 1.4x slower |
| openTelemetryClassic | 859.24 | ± 38.79 | ops/s | 8.3x slower |
| openTelemetryExponential | 643.58 | ± 8.00 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 791.21K | ± 13.69K | ops/s | **fastest** |
| prometheusWriteToNull | 789.06K | ± 11.19K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 755.27K | ± 12.03K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 714.26K | ± 17.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      66413.264   ± 3292.040  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1876.428    ± 256.090  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1803.361    ± 206.905  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1917.458    ± 374.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59607.023   ± 1929.968  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69765.912    ± 197.766  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67776.702    ± 737.022  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10716.314    ± 111.061  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10856.557    ± 170.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11003.388    ± 171.045  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        859.240     ± 38.788  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        643.584      ± 8.001  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7172.905     ± 99.939  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5023.570    ± 387.292  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6763.176    ± 377.636  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     714262.099  ± 17167.133  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     791209.169  ± 13690.809  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     755268.723  ± 12029.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     789056.534  ± 11190.532  ops/s
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
