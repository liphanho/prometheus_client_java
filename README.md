# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-05T09:45:22Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 65.02K | ± 3.02K | ops/s | **fastest** |
| prometheusInc | 64.22K | ± 564.16 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 61.69K | ± 765.13 | ops/s | 1.1x slower |
| prometheusAdd | 58.02K | ± 1.86K | ops/s | 1.1x slower |
| simpleclientInc | 11.03K | ± 81.41 | ops/s | 5.9x slower |
| simpleclientNoLabelsInc | 10.76K | ± 179.46 | ops/s | 6.0x slower |
| simpleclientAdd | 10.48K | ± 205.07 | ops/s | 6.2x slower |
| openTelemetryAdd | 1.97K | ± 262.48 | ops/s | 33x slower |
| openTelemetryInc | 1.91K | ± 52.83 | ops/s | 34x slower |
| openTelemetryIncNoLabels | 1.87K | ± 245.43 | ops/s | 35x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.64K | ± 106.20 | ops/s | **fastest** |
| simpleclient | 7.11K | ± 156.56 | ops/s | 1.1x slower |
| prometheusNative | 4.87K | ± 107.05 | ops/s | 1.6x slower |
| openTelemetryClassic | 917.74 | ± 35.20 | ops/s | 8.3x slower |
| openTelemetryExponential | 728.32 | ± 73.01 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 787.05K | ± 18.06K | ops/s | **fastest** |
| prometheusWriteToNull | 761.83K | ± 29.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 738.53K | ± 19.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 719.48K | ± 33.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61692.192    ± 765.132  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1974.940    ± 262.478  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1905.074     ± 52.826  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1868.609    ± 245.426  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58020.281   ± 1858.521  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64218.059    ± 564.159  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65021.526   ± 3024.917  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10477.473    ± 205.067  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11029.379     ± 81.412  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10763.758    ± 179.457  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        917.738     ± 35.203  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        728.324     ± 73.005  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7637.185    ± 106.200  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4868.272    ± 107.051  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7106.805    ± 156.561  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     719480.225  ± 33733.652  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     738527.154  ± 19251.258  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     787053.804  ± 18057.124  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     761832.068  ± 29327.230  ops/s
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
