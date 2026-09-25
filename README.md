# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-25T08:28:50Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 72.15K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.27K | ± 869.99 | ops/s | 1.1x slower |
| prometheusAdd | 58.17K | ± 1.15K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 52.14K | ± 2.48K | ops/s | 1.4x slower |
| simpleclientInc | 7.35K | ± 238.62 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.29K | ± 253.65 | ops/s | 9.9x slower |
| simpleclientAdd | 7.23K | ± 151.43 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 1.66K | ± 156.06 | ops/s | 43x slower |
| openTelemetryAdd | 1.66K | ± 134.09 | ops/s | 43x slower |
| openTelemetryInc | 1.63K | ± 22.61 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.43K | ± 57.01 | ops/s | **fastest** |
| simpleclient | 5.60K | ± 50.55 | ops/s | 1.1x slower |
| prometheusNative | 3.83K | ± 98.59 | ops/s | 1.7x slower |
| openTelemetryClassic | 716.79 | ± 25.09 | ops/s | 9.0x slower |
| openTelemetryExponential | 609.48 | ± 32.06 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 723.68K | ± 3.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 684.43K | ± 4.89K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 661.41K | ± 5.30K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 660.18K | ± 9.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      52144.179   ± 2480.828  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1659.159    ± 134.087  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1628.089     ± 22.614  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1662.924    ± 156.056  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58169.207   ± 1151.515  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      72150.897   ± 1017.586  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63271.213    ± 869.992  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7234.520    ± 151.430  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7349.748    ± 238.621  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7287.216    ± 253.648  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        716.793     ± 25.086  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        609.478     ± 32.057  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6431.844     ± 57.013  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3830.972     ± 98.588  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5602.125     ± 50.549  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     660176.506   ± 9525.285  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661411.347   ± 5297.598  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     684428.566   ± 4893.312  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     723680.059   ± 3789.718  ops/s
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
