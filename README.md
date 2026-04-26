# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-26T06:29:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 55.94K | ± 712.41 | ops/s | **fastest** |
| prometheusInc | 55.69K | ± 16.36K | ops/s | 1.0x slower |
| prometheusAdd | 51.18K | ± 589.54 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.61K | ± 544.52 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.57K | ± 66.12 | ops/s | 8.5x slower |
| simpleclientInc | 6.47K | ± 109.36 | ops/s | 8.6x slower |
| simpleclientAdd | 6.18K | ± 245.76 | ops/s | 9.0x slower |
| openTelemetryInc | 1.42K | ± 162.47 | ops/s | 39x slower |
| openTelemetryAdd | 1.36K | ± 135.93 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.19K | ± 50.41 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.60K | ± 17.22 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 28.07 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 158.05 | ops/s | 1.9x slower |
| openTelemetryClassic | 646.95 | ± 26.58 | ops/s | 8.7x slower |
| openTelemetryExponential | 569.44 | ± 13.53 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 534.47K | ± 5.99K | ops/s | **fastest** |
| prometheusWriteToNull | 533.78K | ± 2.64K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.15K | ± 5.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.78K | ± 3.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49614.908    ± 544.523  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1361.205    ± 135.929  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1421.597    ± 162.467  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1187.927     ± 50.411  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51180.574    ± 589.536  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      55688.304  ± 16363.440  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55942.092    ± 712.406  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6182.767    ± 245.764  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6471.573    ± 109.360  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6573.585     ± 66.123  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        646.952     ± 26.577  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.441     ± 13.531  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5597.339     ± 17.216  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3009.915    ± 158.049  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.043     ± 28.072  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509780.682   ± 3186.253  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514149.715   ± 5262.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     534471.060   ± 5989.763  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533777.085   ± 2637.750  ops/s
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
