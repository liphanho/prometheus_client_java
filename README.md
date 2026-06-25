# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-25T07:24:51Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.87K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 415.50 | ops/s | 1.1x slower |
| prometheusAdd | 51.35K | ± 564.80 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.55K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientInc | 6.47K | ± 173.16 | ops/s | 10x slower |
| simpleclientAdd | 6.47K | ± 36.64 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 37.83 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 171.44 | ops/s | 46x slower |
| openTelemetryAdd | 1.34K | ± 159.39 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.17K | ± 5.56 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.12K | ± 186.39 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 90.62 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 151.19 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.04 | ± 50.54 | ops/s | 7.5x slower |
| openTelemetryExponential | 558.75 | ± 7.68 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 524.47K | ± 3.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.16K | ± 2.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 507.27K | ± 2.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 497.37K | ± 8.65K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48554.667   ± 1325.456  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1336.249    ± 159.391  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1416.182    ± 171.441  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1173.119      ± 5.563  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51353.519    ± 564.805  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64872.462   ± 1263.335  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57037.465    ± 415.499  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6469.062     ± 36.637  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6473.574    ± 173.161  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6347.346     ± 37.825  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.044     ± 50.536  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.751      ± 7.675  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5115.655    ± 186.389  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3047.907    ± 151.190  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.512     ± 90.619  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     497370.800   ± 8652.144  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     507268.641   ± 2537.180  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517158.472   ± 2026.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     524472.013   ± 3932.019  ops/s
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
