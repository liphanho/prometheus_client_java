# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-06T07:11:21Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.80K | ± 1.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.96K | ± 751.79 | ops/s | 1.2x slower |
| prometheusAdd | 50.90K | ± 460.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.65K | ± 1.86K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 40.77 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.47K | ± 206.44 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 201.93 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 127.18 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.28K | ± 66.59 | ops/s | 51x slower |
| openTelemetryAdd | 1.21K | ± 33.72 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 82.78 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 29.93 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 114.89 | ops/s | 1.9x slower |
| openTelemetryClassic | 637.93 | ± 14.49 | ops/s | 8.6x slower |
| openTelemetryExponential | 562.25 | ± 26.48 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.41K | ± 9.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.47K | ± 7.17K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 504.08K | ± 5.54K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 504.06K | ± 3.35K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48648.232   ± 1863.280  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1205.413     ± 33.723  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1371.024    ± 127.175  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1280.409     ± 66.588  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50900.248    ± 460.625  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64803.321   ± 1296.468  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55961.196    ± 751.787  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6346.670    ± 201.930  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6689.852     ± 40.767  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6472.763    ± 206.441  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        637.933     ± 14.492  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.254     ± 26.481  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5496.085     ± 82.776  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2945.033    ± 114.889  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.985     ± 29.932  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     504076.341   ± 5542.144  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504063.625   ± 3349.840  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527472.889   ± 7165.203  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535410.315   ± 9194.242  ops/s
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
