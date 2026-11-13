# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-13T10:26:34Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.57K | ± 2.33K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.49K | ± 635.29 | ops/s | 1.2x slower |
| prometheusAdd | 63.88K | ± 423.86 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.22K | ± 718.76 | ops/s | 1.3x slower |
| simpleclientInc | 7.90K | ± 147.44 | ops/s | 9.7x slower |
| simpleclientAdd | 7.77K | ± 110.70 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.58K | ± 239.14 | ops/s | 10x slower |
| openTelemetryInc | 1.95K | ± 70.87 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.88K | ± 159.32 | ops/s | 41x slower |
| openTelemetryAdd | 1.78K | ± 70.53 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.86K | ± 616.60 | ops/s | **fastest** |
| simpleclient | 5.78K | ± 83.30 | ops/s | 1.2x slower |
| prometheusNative | 4.02K | ± 92.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 819.72 | ± 32.92 | ops/s | 8.4x slower |
| openTelemetryExponential | 689.11 | ± 34.55 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 731.79K | ± 6.56K | ops/s | **fastest** |
| prometheusWriteToNull | 722.17K | ± 35.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 673.31K | ± 14.64K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 657.89K | ± 10.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57224.920    ± 718.760  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1783.198     ± 70.531  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1945.909     ± 70.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1880.459    ± 159.321  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63881.420    ± 423.857  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76565.033   ± 2331.191  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66492.332    ± 635.294  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7772.950    ± 110.700  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7900.302    ± 147.443  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7580.332    ± 239.144  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        819.717     ± 32.924  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        689.114     ± 34.545  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6855.379    ± 616.596  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4015.793     ± 92.636  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5782.494     ± 83.298  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     657891.800  ± 10164.280  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     673306.463  ± 14639.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     731785.842   ± 6563.271  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     722172.761  ± 35634.545  ops/s
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
