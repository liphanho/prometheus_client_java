# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-12T06:04:07Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 62.74K | ± 4.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 490.36 | ops/s | 1.1x slower |
| prometheusAdd | 51.44K | ± 214.38 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.90K | ± 516.42 | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 179.84 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.53K | ± 92.80 | ops/s | 9.6x slower |
| simpleclientAdd | 6.33K | ± 234.60 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.40K | ± 285.73 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.40K | ± 119.40 | ops/s | 45x slower |
| openTelemetryInc | 1.31K | ± 142.90 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 93.03 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 101.97 | ops/s | 1.2x slower |
| prometheusNative | 3.12K | ± 64.43 | ops/s | 1.7x slower |
| openTelemetryClassic | 706.68 | ± 28.12 | ops/s | 7.5x slower |
| openTelemetryExponential | 557.92 | ± 37.82 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.67K | ± 1.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.83K | ± 7.76K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.33K | ± 12.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.87K | ± 3.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47897.928    ± 516.422  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1403.218    ± 285.730  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.371    ± 142.898  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1398.305    ± 119.396  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51443.730    ± 214.382  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      62741.628   ± 4014.805  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56731.662    ± 490.365  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6332.210    ± 234.600  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6570.350    ± 179.840  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6526.548     ± 92.795  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        706.677     ± 28.118  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.920     ± 37.822  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5270.554     ± 93.034  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3116.021     ± 64.435  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4427.167    ± 101.968  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507873.005   ± 3734.513  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509330.215  ± 12424.955  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527825.832   ± 7757.764  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532667.903   ± 1491.498  ops/s
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
