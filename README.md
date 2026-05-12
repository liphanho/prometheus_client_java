# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-12T06:55:39Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.24K | ± 2.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.35K | ± 732.18 | ops/s | 1.2x slower |
| prometheusAdd | 50.98K | ± 716.44 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.98K | ± 741.79 | ops/s | 1.3x slower |
| simpleclientInc | 6.63K | ± 128.56 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.29K | ± 79.01 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 67.20 | ops/s | 11x slower |
| openTelemetryAdd | 1.36K | ± 185.42 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.26K | ± 90.79 | ops/s | 52x slower |
| openTelemetryInc | 1.22K | ± 33.56 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.10K | ± 210.83 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 13.13 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 219.02 | ops/s | 1.6x slower |
| openTelemetryClassic | 699.34 | ± 41.49 | ops/s | 7.3x slower |
| openTelemetryExponential | 536.33 | ± 14.34 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.27K | ± 6.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.47K | ± 4.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.66K | ± 6.53K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.37K | ± 3.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49978.135    ± 741.792  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1357.746    ± 185.416  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1223.389     ± 33.557  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.374     ± 90.794  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50979.761    ± 716.444  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65236.384   ± 2079.727  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56352.028    ± 732.184  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6030.340     ± 67.199  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6629.985    ± 128.565  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6294.757     ± 79.010  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.340     ± 41.494  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.327     ± 14.339  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5098.202    ± 210.825  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3149.835    ± 219.024  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.347     ± 13.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507371.604   ± 3348.029  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512659.624   ± 6528.022  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527473.778   ± 4771.003  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529270.689   ± 6341.353  ops/s
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
