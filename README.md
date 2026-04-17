# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-17T06:06:23Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.95K | ± 972.90 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.12K | ± 400.63 | ops/s | 1.2x slower |
| prometheusAdd | 47.60K | ± 1.44K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.49K | ± 1.57K | ops/s | 1.4x slower |
| simpleclientInc | 6.17K | ± 163.17 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.09K | ± 259.71 | ops/s | 9.7x slower |
| simpleclientAdd | 6.08K | ± 111.42 | ops/s | 9.7x slower |
| openTelemetryIncNoLabels | 1.48K | ± 114.32 | ops/s | 40x slower |
| openTelemetryAdd | 1.44K | ± 112.72 | ops/s | 41x slower |
| openTelemetryInc | 1.35K | ± 35.52 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.01K | ± 437.05 | ops/s | **fastest** |
| simpleclient | 4.22K | ± 49.08 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 128.11 | ops/s | 1.6x slower |
| openTelemetryClassic | 647.16 | ± 32.46 | ops/s | 7.7x slower |
| openTelemetryExponential | 508.86 | ± 8.98 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 642.13K | ± 10.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 626.71K | ± 2.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 608.31K | ± 3.37K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 594.25K | ± 7.77K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43491.681   ± 1570.797  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1441.813    ± 112.725  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1348.680     ± 35.522  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1477.698    ± 114.317  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47597.535   ± 1437.700  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58949.800    ± 972.904  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51116.400    ± 400.630  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6080.909    ± 111.420  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6170.392    ± 163.165  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6086.743    ± 259.710  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        647.161     ± 32.457  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        508.856      ± 8.979  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5007.916    ± 437.047  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3127.480    ± 128.112  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4222.403     ± 49.077  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     594249.134   ± 7773.361  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     608308.493   ± 3368.790  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     626710.640   ± 2340.420  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     642125.552  ± 10923.587  ops/s
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
