# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-18T05:39:48Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.13K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.47K | ± 591.25 | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 110.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.14K | ± 1.06K | ops/s | 1.4x slower |
| simpleclientInc | 6.79K | ± 7.09 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.62K | ± 139.68 | ops/s | 9.8x slower |
| simpleclientAdd | 6.53K | ± 16.56 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.48K | ± 169.70 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.33K | ± 88.14 | ops/s | 49x slower |
| openTelemetryInc | 1.20K | ± 18.50 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 468.98 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 82.10 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 238.00 | ops/s | 1.8x slower |
| openTelemetryClassic | 687.14 | ± 14.90 | ops/s | 8.1x slower |
| openTelemetryExponential | 546.67 | ± 23.31 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 547.45K | ± 3.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 541.54K | ± 3.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.35K | ± 8.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.50K | ± 2.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48144.286   ± 1057.588  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1477.403    ± 169.700  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1195.840     ± 18.497  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.832     ± 88.135  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51595.257    ± 110.880  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65132.179   ± 1201.557  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56466.336    ± 591.247  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6527.845     ± 16.564  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6794.004      ± 7.090  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6618.578    ± 139.681  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.140     ± 14.895  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.668     ± 23.312  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5551.619    ± 468.980  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3161.851    ± 237.996  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4564.189     ± 82.098  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521502.354   ± 2335.147  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522349.796   ± 8935.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541543.688   ± 3365.861  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     547447.190   ± 3916.616  ops/s
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
