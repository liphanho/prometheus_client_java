# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T08:40:17Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.32K | ± 725.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.20K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 62.68K | ± 1.42K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.04K | ± 728.09 | ops/s | 1.3x slower |
| simpleclientInc | 7.82K | ± 174.82 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.61K | ± 106.68 | ops/s | 10x slower |
| simpleclientAdd | 7.44K | ± 471.39 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.78K | ± 81.43 | ops/s | 43x slower |
| openTelemetryAdd | 1.77K | ± 97.79 | ops/s | 43x slower |
| openTelemetryInc | 1.71K | ± 34.37 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.89K | ± 57.21 | ops/s | **fastest** |
| simpleclient | 5.64K | ± 35.73 | ops/s | 1.2x slower |
| prometheusNative | 4.05K | ± 101.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 749.81 | ± 13.53 | ops/s | 9.2x slower |
| openTelemetryExponential | 652.33 | ± 8.41 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 772.83K | ± 2.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 750.48K | ± 7.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 725.43K | ± 5.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 717.67K | ± 5.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57042.616    ± 728.094  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1774.168     ± 97.792  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1705.683     ± 34.368  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1775.497     ± 81.427  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62682.081   ± 1420.502  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76317.086    ± 725.866  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66203.358   ± 1065.204  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7441.592    ± 471.386  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7821.904    ± 174.822  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7614.789    ± 106.679  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.807     ± 13.529  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        652.326      ± 8.410  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6887.261     ± 57.214  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4048.470    ± 101.084  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5641.065     ± 35.734  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     717670.623   ± 5280.573  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     725426.172   ± 5727.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     750478.133   ± 7535.188  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772831.425   ± 2926.500  ops/s
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
