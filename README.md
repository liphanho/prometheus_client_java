# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-23T05:46:18Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.03K | ± 978.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 481.53 | ops/s | 1.2x slower |
| prometheusAdd | 48.20K | ± 565.69 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.68K | ± 801.76 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.41K | ± 12.38 | ops/s | 9.4x slower |
| simpleclientInc | 6.37K | ± 6.06 | ops/s | 9.4x slower |
| simpleclientAdd | 6.10K | ± 149.06 | ops/s | 9.8x slower |
| openTelemetryInc | 1.41K | ± 107.07 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.37K | ± 59.80 | ops/s | 44x slower |
| openTelemetryAdd | 1.36K | ± 79.08 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.52K | ± 109.96 | ops/s | **fastest** |
| prometheusClassic | 4.34K | ± 703.60 | ops/s | 1.0x slower |
| prometheusNative | 3.05K | ± 55.43 | ops/s | 1.5x slower |
| openTelemetryClassic | 629.30 | ± 26.68 | ops/s | 7.2x slower |
| openTelemetryExponential | 541.65 | ± 17.82 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 620.41K | ± 3.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 604.32K | ± 2.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 584.34K | ± 6.07K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 576.77K | ± 5.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44677.105    ± 801.755  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1357.677     ± 79.080  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1409.025    ± 107.067  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1368.212     ± 59.799  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48196.718    ± 565.694  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60034.064    ± 978.123  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51556.067    ± 481.527  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6102.605    ± 149.056  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6371.488      ± 6.055  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6405.531     ± 12.383  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        629.302     ± 26.683  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.646     ± 17.816  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4338.131    ± 703.597  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3054.300     ± 55.428  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4517.078    ± 109.957  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     576765.679   ± 5597.730  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     584335.159   ± 6065.970  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     604324.332   ± 2815.447  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     620407.727   ± 3245.102  ops/s
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
