# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T05:29:06Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.93K | ± 1.64K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.08K | ± 1.13K | ops/s | 1.1x slower |
| prometheusAdd | 48.81K | ± 829.60 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.27K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.22K | ± 54.53 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.95K | ± 262.31 | ops/s | 9.7x slower |
| simpleclientAdd | 5.65K | ± 165.25 | ops/s | 10x slower |
| openTelemetryAdd | 1.32K | ± 90.34 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.27K | ± 57.95 | ops/s | 45x slower |
| openTelemetryInc | 1.25K | ± 12.89 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 64.02 | ops/s | **fastest** |
| prometheusClassic | 4.19K | ± 318.40 | ops/s | 1.1x slower |
| prometheusNative | 3.03K | ± 70.74 | ops/s | 1.5x slower |
| openTelemetryClassic | 573.63 | ± 5.14 | ops/s | 7.9x slower |
| openTelemetryExponential | 516.77 | ± 17.88 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 643.37K | ± 4.84K | ops/s | **fastest** |
| prometheusWriteToByteArray | 629.60K | ± 7.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 605.24K | ± 3.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 599.22K | ± 3.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43268.974   ± 1280.825  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1315.369     ± 90.345  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1250.527     ± 12.888  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1274.324     ± 57.955  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48813.315    ± 829.597  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57927.993   ± 1635.778  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51075.292   ± 1133.536  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5650.339    ± 165.254  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6224.123     ± 54.529  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5951.501    ± 262.307  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        573.631      ± 5.138  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        516.768     ± 17.882  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4194.401    ± 318.402  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3033.700     ± 70.739  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4511.306     ± 64.020  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     599223.474   ± 3406.135  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     605236.422   ± 3436.224  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     629600.765   ± 7202.764  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     643374.026   ± 4837.466  ops/s
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
