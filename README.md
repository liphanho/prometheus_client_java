# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-30T06:25:58Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.91K | ± 2.43K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.68K | ± 692.88 | ops/s | 1.1x slower |
| prometheusAdd | 47.82K | ± 451.17 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.98K | ± 173.64 | ops/s | 1.3x slower |
| simpleclientInc | 6.24K | ± 22.80 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.00K | ± 270.06 | ops/s | 9.7x slower |
| simpleclientAdd | 5.95K | ± 196.93 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.40K | ± 97.29 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.33K | ± 58.34 | ops/s | 43x slower |
| openTelemetryInc | 1.32K | ± 30.26 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 31.79 | ops/s | **fastest** |
| simpleclient | 4.59K | ± 71.29 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 53.61 | ops/s | 1.8x slower |
| openTelemetryClassic | 593.20 | ± 21.64 | ops/s | 9.3x slower |
| openTelemetryExponential | 514.24 | ± 21.58 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 618.06K | ± 2.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.33K | ± 6.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 582.63K | ± 5.84K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 574.33K | ± 3.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43977.664    ± 173.640  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1399.258     ± 97.291  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1323.623     ± 30.262  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1334.879     ± 58.341  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47815.363    ± 451.171  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57912.771   ± 2428.759  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51678.749    ± 692.878  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5948.239    ± 196.931  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6242.930     ± 22.802  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6000.432    ± 270.061  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        593.205     ± 21.636  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.242     ± 21.576  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5499.749     ± 31.794  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3134.610     ± 53.610  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4588.932     ± 71.295  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     574329.631   ± 3439.221  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     582631.944   ± 5844.540  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609327.096   ± 6075.040  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     618064.951   ± 2366.243  ops/s
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
