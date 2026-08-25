# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-25T04:15:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 115.53 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.13K | ± 118.36 | ops/s | 1.2x slower |
| prometheusAdd | 51.09K | ± 657.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.84K | ± 1.40K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 54.27 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.48K | ± 183.90 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 205.67 | ops/s | 11x slower |
| openTelemetryAdd | 1.55K | ± 282.35 | ops/s | 42x slower |
| openTelemetryInc | 1.32K | ± 21.14 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.26K | ± 27.18 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.21K | ± 193.80 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 42.10 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 63.46 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.66 | ± 26.55 | ops/s | 7.6x slower |
| openTelemetryExponential | 589.18 | ± 28.79 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 528.98K | ± 6.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.05K | ± 4.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 511.71K | ± 6.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.50K | ± 8.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48844.710   ± 1397.528  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1552.187    ± 282.354  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.826     ± 21.138  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.124     ± 27.185  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51089.866    ± 657.809  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65815.029    ± 115.535  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57129.357    ± 118.356  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.902    ± 205.673  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6608.486     ± 54.266  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6475.207    ± 183.902  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.657     ± 26.552  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.183     ± 28.794  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5207.967    ± 193.797  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.699     ± 63.459  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4368.407     ± 42.096  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506497.098   ± 8660.041  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     511707.852   ± 6108.020  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525047.323   ± 4457.650  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     528977.339   ± 6564.354  ops/s
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
