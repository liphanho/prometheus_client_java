# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-21T06:37:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.17K | ± 174.31 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.06K | ± 515.44 | ops/s | 1.2x slower |
| prometheusAdd | 60.60K | ± 2.04K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.71K | ± 219.80 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 7.91K | ± 252.64 | ops/s | 9.8x slower |
| simpleclientInc | 7.86K | ± 363.04 | ops/s | 9.8x slower |
| simpleclientAdd | 7.68K | ± 230.11 | ops/s | 10x slower |
| openTelemetryAdd | 1.88K | ± 218.42 | ops/s | 41x slower |
| openTelemetryInc | 1.84K | ± 141.84 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.79K | ± 136.79 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.14K | ± 529.76 | ops/s | **fastest** |
| simpleclient | 5.88K | ± 66.94 | ops/s | 1.0x slower |
| prometheusNative | 4.01K | ± 134.46 | ops/s | 1.5x slower |
| openTelemetryClassic | 771.17 | ± 14.07 | ops/s | 8.0x slower |
| openTelemetryExponential | 667.75 | ± 4.27 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 763.71K | ± 4.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 754.03K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 720.89K | ± 8.16K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 716.19K | ± 3.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56705.091    ± 219.796  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1875.051    ± 218.423  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1841.326    ± 141.838  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1789.396    ± 136.793  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      60596.548   ± 2040.806  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77168.023    ± 174.314  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66055.559    ± 515.437  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7683.977    ± 230.109  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7859.433    ± 363.036  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7911.118    ± 252.641  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        771.173     ± 14.075  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        667.750      ± 4.275  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6138.917    ± 529.763  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4014.639    ± 134.460  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5882.582     ± 66.941  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     716185.894   ± 3736.566  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     720888.728   ± 8162.015  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     754034.815   ± 3650.485  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     763714.533   ± 4702.252  ops/s
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
