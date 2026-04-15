# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-15T06:02:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.28K | ± 1.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.56K | ± 436.45 | ops/s | 1.2x slower |
| prometheusAdd | 51.42K | ± 279.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.25K | ± 1.55K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 138.82 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.40K | ± 174.43 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 260.65 | ops/s | 11x slower |
| openTelemetryAdd | 1.37K | ± 193.43 | ops/s | 47x slower |
| openTelemetryInc | 1.26K | ± 25.05 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.24K | ± 13.25 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 115.71 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 41.38 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 168.90 | ops/s | 1.8x slower |
| openTelemetryClassic | 676.41 | ± 14.23 | ops/s | 7.8x slower |
| openTelemetryExponential | 600.56 | ± 28.66 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.61K | ± 3.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.95K | ± 6.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.94K | ± 12.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 501.51K | ± 2.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49252.334   ± 1554.707  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1374.402    ± 193.430  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.606     ± 25.051  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1242.948     ± 13.254  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51423.091    ± 279.665  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65282.137   ± 1532.507  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56563.262    ± 436.451  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6160.518    ± 260.649  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.689    ± 138.818  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6404.888    ± 174.433  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.409     ± 14.227  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        600.557     ± 28.661  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5290.892    ± 115.712  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2958.083    ± 168.901  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4379.452     ± 41.382  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501506.922   ± 2718.364  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509936.998  ± 12884.538  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524948.573   ± 6807.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527612.785   ± 3677.123  ops/s
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
