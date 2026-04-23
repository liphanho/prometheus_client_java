# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-23T06:07:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 434.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.52K | ± 923.89 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 629.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.64K | ± 1.69K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 182.67 | ops/s | 10.0x slower |
| simpleclientAdd | 6.46K | ± 17.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 165.98 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 103.93 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.33K | ± 149.80 | ops/s | 49x slower |
| openTelemetryAdd | 1.27K | ± 40.08 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 382.11 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 58.96 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 166.65 | ops/s | 1.8x slower |
| openTelemetryClassic | 686.66 | ± 57.71 | ops/s | 7.7x slower |
| openTelemetryExponential | 574.70 | ± 43.87 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 544.38K | ± 10.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 536.68K | ± 11.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.36K | ± 3.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 501.81K | ± 4.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49643.810   ± 1688.460  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1271.106     ± 40.079  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1461.773    ± 103.934  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1327.606    ± 149.797  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51051.097    ± 629.179  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65587.050    ± 434.549  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56523.558    ± 923.890  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6458.300     ± 17.941  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.459    ± 182.673  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6444.516    ± 165.975  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.656     ± 57.710  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.697     ± 43.870  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5273.616    ± 382.112  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2963.547    ± 166.651  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.909     ± 58.958  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501809.764   ± 4680.792  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509357.981   ± 3634.926  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     536681.964  ± 11588.625  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     544376.109  ± 10005.734  ops/s
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
