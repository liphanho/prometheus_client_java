# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-18T08:10:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.72K | ± 75.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.53K | ± 3.61K | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 121.00 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.53K | ± 614.78 | ops/s | 1.3x slower |
| simpleclientInc | 6.49K | ± 161.13 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 20.44 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 184.76 | ops/s | 10x slower |
| openTelemetryAdd | 1.53K | ± 159.10 | ops/s | 43x slower |
| openTelemetryInc | 1.39K | ± 155.82 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.25K | ± 13.34 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 10.48 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 41.80 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 110.74 | ops/s | 1.7x slower |
| openTelemetryClassic | 697.22 | ± 34.20 | ops/s | 7.6x slower |
| openTelemetryExponential | 564.12 | ± 28.88 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.39K | ± 4.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.49K | ± 7.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.58K | ± 2.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 518.59K | ± 4.44K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50534.640    ± 614.775  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1532.612    ± 159.099  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1393.999    ± 155.822  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1254.728     ± 13.344  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51445.153    ± 121.002  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65715.650     ± 75.279  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54533.794   ± 3610.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6460.247     ± 20.445  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6487.287    ± 161.134  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6372.406    ± 184.758  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.224     ± 34.202  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.118     ± 28.876  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5288.987     ± 10.481  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3069.680    ± 110.739  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.383     ± 41.797  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518592.969   ± 4435.920  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519581.261   ± 2882.966  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533485.930   ± 7373.067  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535393.865   ± 4981.740  ops/s
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
