# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-02T05:47:24Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.72K | ± 1.87K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.26K | ± 436.12 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 276.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.85K | ± 604.30 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.42K | ± 172.43 | ops/s | 10x slower |
| simpleclientInc | 6.38K | ± 289.62 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 240.17 | ops/s | 10x slower |
| openTelemetryInc | 1.41K | ± 176.10 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.24K | ± 85.65 | ops/s | 52x slower |
| openTelemetryAdd | 1.19K | ± 36.67 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.43K | ± 290.65 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 53.89 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 161.96 | ops/s | 1.8x slower |
| openTelemetryClassic | 722.38 | ± 35.51 | ops/s | 7.5x slower |
| openTelemetryExponential | 560.89 | ± 27.66 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 530.55K | ± 5.73K | ops/s | **fastest** |
| prometheusWriteToNull | 526.73K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.89K | ± 5.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 501.22K | ± 5.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49845.743    ± 604.295  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1191.785     ± 36.673  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.350    ± 176.097  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1240.036     ± 85.650  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51428.292    ± 276.712  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64718.616   ± 1866.595  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56256.124    ± 436.119  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6317.716    ± 240.168  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6377.979    ± 289.620  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6422.930    ± 172.428  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        722.383     ± 35.510  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.887     ± 27.665  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5428.922    ± 290.645  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3067.293    ± 161.962  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.701     ± 53.890  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     501215.916   ± 5254.186  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509894.070   ± 5838.518  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530553.680   ± 5727.478  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     526725.242   ± 5055.450  ops/s
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
