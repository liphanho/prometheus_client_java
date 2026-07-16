# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T06:28:07Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.63K | ± 787.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 320.09 | ops/s | 1.2x slower |
| prometheusAdd | 49.24K | ± 3.51K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.85K | ± 1.32K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.57K | ± 52.77 | ops/s | 10.0x slower |
| simpleclientInc | 6.55K | ± 202.52 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 216.02 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 289.87 | ops/s | 46x slower |
| openTelemetryInc | 1.36K | ± 99.14 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.29K | ± 167.32 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 205.18 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 11.21 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 76.97 | ops/s | 1.7x slower |
| openTelemetryClassic | 687.83 | ± 26.23 | ops/s | 7.8x slower |
| openTelemetryExponential | 563.47 | ± 27.12 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 518.31K | ± 5.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 514.66K | ± 7.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 502.18K | ± 4.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.47K | ± 4.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48851.387   ± 1324.151  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1420.631    ± 289.869  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1356.745     ± 99.138  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1292.312    ± 167.323  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49244.160   ± 3512.217  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65634.684    ± 787.276  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56798.649    ± 320.090  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6196.944    ± 216.019  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.446    ± 202.517  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6568.689     ± 52.772  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.825     ± 26.229  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.469     ± 27.123  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5340.044    ± 205.179  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.844     ± 76.971  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.600     ± 11.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499472.603   ± 4891.470  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     502182.100   ± 4802.009  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     514661.753   ± 7836.457  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     518311.591   ± 5605.360  ops/s
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
