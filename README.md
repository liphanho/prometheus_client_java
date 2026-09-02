# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-02T08:08:49Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.98K | ± 1.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.63K | ± 425.02 | ops/s | 1.1x slower |
| prometheusAdd | 51.64K | ± 158.11 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.49K | ± 1.29K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 190.52 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.50K | ± 135.21 | ops/s | 10.0x slower |
| simpleclientAdd | 6.28K | ± 223.84 | ops/s | 10x slower |
| openTelemetryInc | 1.33K | ± 173.20 | ops/s | 49x slower |
| openTelemetryAdd | 1.29K | ± 30.14 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 9.81 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 63.46 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 52.77 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 141.49 | ops/s | 1.7x slower |
| openTelemetryClassic | 669.13 | ± 14.15 | ops/s | 7.9x slower |
| openTelemetryExponential | 556.72 | ± 37.50 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 514.79K | ± 6.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 514.00K | ± 5.15K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 499.71K | ± 3.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 497.89K | ± 6.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48493.338   ± 1292.792  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1285.280     ± 30.141  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1333.878    ± 173.200  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.508      ± 9.807  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51638.174    ± 158.109  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64981.202   ± 1860.113  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56629.367    ± 425.022  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6279.673    ± 223.839  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6580.949    ± 190.522  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6500.605    ± 135.210  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        669.133     ± 14.148  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.722     ± 37.498  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5267.036     ± 63.457  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.768    ± 141.486  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.692     ± 52.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499708.292   ± 3662.233  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     497886.827   ± 6102.594  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513996.358   ± 5153.702  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     514789.215   ± 6315.273  ops/s
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
