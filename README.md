# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-17T05:38:16Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.15K | ± 1.52K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 308.83 | ops/s | 1.1x slower |
| prometheusAdd | 50.54K | ± 1.61K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.53K | ± 1.40K | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 26.68 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.70K | ± 12.73 | ops/s | 9.7x slower |
| simpleclientAdd | 6.30K | ± 195.07 | ops/s | 10x slower |
| openTelemetryAdd | 1.65K | ± 98.40 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.29K | ± 89.83 | ops/s | 50x slower |
| openTelemetryInc | 1.18K | ± 34.11 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.19K | ± 247.57 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 41.38 | ops/s | 1.1x slower |
| prometheusNative | 3.13K | ± 88.90 | ops/s | 1.7x slower |
| openTelemetryClassic | 722.59 | ± 34.09 | ops/s | 7.2x slower |
| openTelemetryExponential | 566.74 | ± 11.51 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.45K | ± 10.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 508.22K | ± 5.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.51K | ± 8.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.30K | ± 2.96K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48531.614   ± 1403.181  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1647.470     ± 98.403  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1181.383     ± 34.105  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1293.059     ± 89.832  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50544.167   ± 1610.206  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65152.774   ± 1517.007  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56956.708    ± 308.831  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6300.828    ± 195.068  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6765.644     ± 26.682  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6703.136     ± 12.727  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        722.593     ± 34.092  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.743     ± 11.514  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5193.066    ± 247.573  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3128.978     ± 88.905  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.159     ± 41.380  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507295.971   ± 2964.429  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507511.905   ± 8471.325  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     508216.429   ± 5543.661  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529452.275  ± 10848.659  ops/s
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
