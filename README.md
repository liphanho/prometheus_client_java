# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-25T05:39:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.50K | ± 3.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 905.38 | ops/s | 1.1x slower |
| prometheusAdd | 51.26K | ± 239.12 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.89K | ± 672.73 | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 23.97 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.55K | ± 195.81 | ops/s | 9.7x slower |
| simpleclientAdd | 6.32K | ± 138.08 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.41K | ± 231.24 | ops/s | 45x slower |
| openTelemetryInc | 1.31K | ± 14.11 | ops/s | 48x slower |
| openTelemetryAdd | 1.27K | ± 69.66 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 134.25 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 58.13 | ops/s | 1.2x slower |
| prometheusNative | 2.98K | ± 114.43 | ops/s | 1.8x slower |
| openTelemetryClassic | 658.60 | ± 14.59 | ops/s | 8.2x slower |
| openTelemetryExponential | 568.37 | ± 12.80 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.63K | ± 7.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 533.10K | ± 6.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 523.95K | ± 2.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 515.15K | ± 3.19K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47888.934    ± 672.730  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1270.306     ± 69.662  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1311.512     ± 14.111  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1413.909    ± 231.245  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51263.499    ± 239.117  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63502.508   ± 3761.283  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56247.259    ± 905.376  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.651    ± 138.080  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6766.277     ± 23.967  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6551.160    ± 195.811  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        658.600     ± 14.591  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.367     ± 12.805  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5393.927    ± 134.254  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2984.651    ± 114.433  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4534.082     ± 58.126  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515147.293   ± 3187.775  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     523950.169   ± 2940.509  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533097.990   ± 6427.124  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541632.517   ± 7956.262  ops/s
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
