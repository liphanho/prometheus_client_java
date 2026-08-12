# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-12T05:24:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.99K | ± 274.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.33K | ± 1.22K | ops/s | 1.2x slower |
| prometheusAdd | 51.56K | ± 193.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.13K | ± 2.54K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 8.33 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.36K | ± 196.52 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 260.72 | ops/s | 11x slower |
| openTelemetryAdd | 1.67K | ± 54.54 | ops/s | 39x slower |
| openTelemetryInc | 1.35K | ± 115.46 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.18K | ± 71.13 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.32K | ± 92.65 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 37.36 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 126.02 | ops/s | 1.7x slower |
| openTelemetryClassic | 722.95 | ± 11.69 | ops/s | 7.4x slower |
| openTelemetryExponential | 551.70 | ± 12.62 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.41K | ± 9.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 518.26K | ± 10.92K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 502.34K | ± 7.26K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 498.68K | ± 3.84K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49127.726   ± 2537.737  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1671.180     ± 54.539  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1353.654    ± 115.459  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1178.891     ± 71.129  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51555.612    ± 193.611  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65992.593    ± 274.485  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56330.457   ± 1219.276  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6262.890    ± 260.718  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6695.420      ± 8.329  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.398    ± 196.516  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        722.952     ± 11.695  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.701     ± 12.621  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5321.604     ± 92.651  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3061.322    ± 126.021  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.330     ± 37.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     502342.108   ± 7255.118  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     498684.826   ± 3838.930  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     518258.345  ± 10922.621  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530410.260   ± 9677.098  ops/s
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
