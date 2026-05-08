# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-08T06:10:33Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.52K | ± 1.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.17K | ± 528.75 | ops/s | 1.1x slower |
| prometheusAdd | 62.46K | ± 255.16 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.82K | ± 226.09 | ops/s | 1.3x slower |
| simpleclientInc | 8.02K | ± 168.56 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.68K | ± 358.19 | ops/s | 10.0x slower |
| simpleclientAdd | 7.23K | ± 316.03 | ops/s | 11x slower |
| openTelemetryAdd | 1.93K | ± 166.20 | ops/s | 40x slower |
| openTelemetryInc | 1.72K | ± 47.84 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.70K | ± 120.78 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.57K | ± 564.73 | ops/s | **fastest** |
| simpleclient | 5.57K | ± 185.43 | ops/s | 1.2x slower |
| prometheusNative | 4.10K | ± 167.65 | ops/s | 1.6x slower |
| openTelemetryClassic | 777.18 | ± 33.66 | ops/s | 8.4x slower |
| openTelemetryExponential | 671.33 | ± 34.72 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 772.83K | ± 7.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 760.95K | ± 6.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 722.62K | ± 3.47K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 717.24K | ± 3.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56815.452    ± 226.088  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1931.103    ± 166.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1721.103     ± 47.837  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1697.215    ± 120.779  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62458.949    ± 255.160  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76520.234   ± 1287.880  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67165.631    ± 528.745  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7230.356    ± 316.028  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8015.916    ± 168.558  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7679.162    ± 358.186  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        777.175     ± 33.664  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        671.331     ± 34.725  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6565.298    ± 564.725  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4097.095    ± 167.651  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5571.823    ± 185.429  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     717244.220   ± 3475.218  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     722618.076   ± 3472.507  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     760947.218   ± 6394.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772825.106   ± 7983.506  ops/s
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
