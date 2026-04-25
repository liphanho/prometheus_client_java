# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-25T05:53:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.16K | ± 1.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.04K | ± 1.20K | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 228.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.14K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 60.61 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 192.89 | ops/s | 10x slower |
| simpleclientAdd | 6.45K | ± 23.32 | ops/s | 10x slower |
| openTelemetryAdd | 1.38K | ± 242.51 | ops/s | 47x slower |
| openTelemetryInc | 1.33K | ± 124.36 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 20.55 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.46K | ± 79.32 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 52.32 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 137.82 | ops/s | 1.8x slower |
| openTelemetryClassic | 686.98 | ± 37.65 | ops/s | 7.9x slower |
| openTelemetryExponential | 559.34 | ± 9.52 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 520.92K | ± 4.08K | ops/s | **fastest** |
| openMetricsWriteToNull | 504.01K | ± 5.36K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 501.78K | ± 12.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.97K | ± 17.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48143.744   ± 1633.700  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1375.781    ± 242.506  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1329.817    ± 124.358  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1213.288     ± 20.553  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51445.188    ± 228.932  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65163.105   ± 1300.193  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56040.341   ± 1199.785  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6449.476     ± 23.321  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6587.901     ± 60.610  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6475.270    ± 192.885  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.983     ± 37.648  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.335      ± 9.521  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5458.911     ± 79.317  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2969.285    ± 137.822  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4403.310     ± 52.322  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495969.632  ± 17752.904  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504009.439   ± 5356.559  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     501779.562  ± 12129.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     520917.605   ± 4079.089  ops/s
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
