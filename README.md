# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-02T06:28:43Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.69K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 1.04K | ops/s | 1.1x slower |
| prometheusAdd | 48.30K | ± 1.09K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.28K | ± 5.51K | ops/s | 1.5x slower |
| simpleclientInc | 6.20K | ± 15.26 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.11K | ± 246.98 | ops/s | 9.6x slower |
| simpleclientAdd | 6.02K | ± 143.05 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.43K | ± 122.20 | ops/s | 41x slower |
| openTelemetryInc | 1.41K | ± 40.40 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.38K | ± 173.76 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 431.48 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 39.52 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 80.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 622.37 | ± 3.52 | ops/s | 8.4x slower |
| openTelemetryExponential | 550.69 | ± 12.28 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 649.37K | ± 7.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 631.89K | ± 4.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 613.55K | ± 4.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 599.19K | ± 8.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40277.934   ± 5513.696  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1428.661    ± 122.199  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1409.422     ± 40.398  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1377.019    ± 173.760  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48302.230   ± 1092.259  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58691.466   ± 1262.961  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51468.361   ± 1037.670  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6023.664    ± 143.052  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6195.848     ± 15.261  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6109.321    ± 246.984  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        622.366      ± 3.522  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.694     ± 12.279  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5252.715    ± 431.485  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3090.854     ± 80.077  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.237     ± 39.522  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     599187.749   ± 8532.828  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     613553.529   ± 4731.365  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     631886.966   ± 4970.098  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     649368.041   ± 7347.542  ops/s
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
