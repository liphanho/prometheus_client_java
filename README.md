# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-19T06:07:57Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.74K | ± 1.27K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.13K | ± 335.23 | ops/s | 1.1x slower |
| prometheusAdd | 48.51K | ± 1.06K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.87K | ± 1.19K | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 142.86 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.14K | ± 209.23 | ops/s | 9.6x slower |
| simpleclientAdd | 5.95K | ± 268.78 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.37K | ± 35.98 | ops/s | 43x slower |
| openTelemetryInc | 1.36K | ± 77.33 | ops/s | 43x slower |
| openTelemetryAdd | 1.34K | ± 46.57 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 461.14 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 32.98 | ops/s | 1.2x slower |
| prometheusNative | 3.20K | ± 44.50 | ops/s | 1.7x slower |
| openTelemetryClassic | 651.09 | ± 14.44 | ops/s | 8.1x slower |
| openTelemetryExponential | 527.89 | ± 27.03 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 636.68K | ± 5.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 630.71K | ± 13.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 606.82K | ± 4.87K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 593.19K | ± 7.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43871.302   ± 1192.674  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1341.452     ± 46.574  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1355.852     ± 77.328  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1370.545     ± 35.982  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48508.542   ± 1058.153  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58738.507   ± 1270.959  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51130.212    ± 335.227  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5952.414    ± 268.784  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6159.972    ± 142.856  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6140.643    ± 209.229  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.090     ± 14.439  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.889     ± 27.034  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5291.334    ± 461.145  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3202.258     ± 44.497  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4369.029     ± 32.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     593194.005   ± 7568.716  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     606816.528   ± 4866.676  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     630712.227  ± 13058.592  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     636676.813   ± 5199.199  ops/s
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
