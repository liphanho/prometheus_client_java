# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-30T06:02:28Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.83K | ± 117.08 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.98K | ± 700.99 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 253.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 40.22K | ± 12.77K | ops/s | 1.6x slower |
| simpleclientInc | 6.69K | ± 55.43 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.62K | ± 7.64 | ops/s | 9.9x slower |
| simpleclientAdd | 6.13K | ± 318.49 | ops/s | 11x slower |
| openTelemetryAdd | 1.46K | ± 243.78 | ops/s | 45x slower |
| openTelemetryInc | 1.34K | ± 143.89 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.22K | ± 100.62 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 24.28 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 67.47 | ops/s | 1.1x slower |
| prometheusNative | 3.04K | ± 211.87 | ops/s | 1.7x slower |
| openTelemetryClassic | 737.90 | ± 44.47 | ops/s | 6.8x slower |
| openTelemetryExponential | 549.53 | ± 16.09 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 546.11K | ± 11.04K | ops/s | **fastest** |
| prometheusWriteToNull | 544.33K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.63K | ± 4.92K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.90K | ± 4.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40223.626  ± 12765.612  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1458.488    ± 243.778  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1337.970    ± 143.891  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1217.693    ± 100.616  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51452.951    ± 253.857  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65834.832    ± 117.076  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55976.279    ± 700.991  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6133.409    ± 318.492  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6686.550     ± 55.427  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6621.661      ± 7.639  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        737.897     ± 44.466  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.532     ± 16.089  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5030.098     ± 24.283  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3042.792    ± 211.869  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.913     ± 67.472  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519900.743   ± 4717.819  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520630.089   ± 4923.802  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     546106.581  ± 11037.679  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     544330.302   ± 3081.597  ops/s
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
