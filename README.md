# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-13T06:31:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.98K | ± 1.98K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.36K | ± 84.34 | ops/s | 1.2x slower |
| prometheusAdd | 51.48K | ± 124.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.49K | ± 2.30K | ops/s | 1.4x slower |
| simpleclientInc | 6.48K | ± 259.82 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.48K | ± 216.76 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 267.28 | ops/s | 10x slower |
| openTelemetryAdd | 1.45K | ± 187.42 | ops/s | 45x slower |
| openTelemetryInc | 1.28K | ± 43.05 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.25K | ± 52.62 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.31K | ± 332.70 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 30.62 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 136.99 | ops/s | 1.7x slower |
| openTelemetryClassic | 673.62 | ± 28.22 | ops/s | 7.9x slower |
| openTelemetryExponential | 562.14 | ± 25.75 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 527.84K | ± 3.18K | ops/s | **fastest** |
| prometheusWriteToNull | 527.62K | ± 5.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.10K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 496.87K | ± 4.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47488.362   ± 2296.904  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1452.829    ± 187.422  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.658     ± 43.051  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1245.515     ± 52.625  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51482.079    ± 124.622  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64981.357   ± 1983.044  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56363.947     ± 84.336  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.809    ± 267.280  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6482.865    ± 259.817  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.029    ± 216.764  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.625     ± 28.217  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.140     ± 25.751  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5312.948    ± 332.703  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3088.082    ± 136.989  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.343     ± 30.616  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     496870.694   ± 4291.345  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512101.625   ± 4793.282  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527842.203   ± 3175.789  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527618.420   ± 5633.892  ops/s
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
