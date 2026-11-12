# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-12T10:38:59Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.98K | ± 1.17K | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.83K | ± 373.37 | ops/s | 1.0x slower |
| prometheusAdd | 55.06K | ± 471.16 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 53.94K | ± 10.45K | ops/s | 1.2x slower |
| simpleclientInc | 10.55K | ± 111.19 | ops/s | 6.3x slower |
| simpleclientNoLabelsInc | 10.24K | ± 220.56 | ops/s | 6.4x slower |
| simpleclientAdd | 10.20K | ± 523.54 | ops/s | 6.5x slower |
| openTelemetryAdd | 1.86K | ± 46.44 | ops/s | 36x slower |
| openTelemetryInc | 1.84K | ± 37.00 | ops/s | 36x slower |
| openTelemetryIncNoLabels | 1.76K | ± 54.68 | ops/s | 37x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.32K | ± 84.76 | ops/s | **fastest** |
| simpleclient | 6.82K | ± 110.34 | ops/s | 1.1x slower |
| prometheusNative | 5.07K | ± 310.22 | ops/s | 1.4x slower |
| openTelemetryClassic | 860.00 | ± 24.27 | ops/s | 8.5x slower |
| openTelemetryExponential | 687.26 | ± 24.25 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 752.34K | ± 65.89K | ops/s | **fastest** |
| openMetricsWriteToNull | 710.22K | ± 80.74K | ops/s | 1.1x slower |
| prometheusWriteToNull | 704.07K | ± 30.00K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 680.95K | ± 19.45K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      53944.719  ± 10451.315  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1856.302     ± 46.444  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1841.078     ± 37.004  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1761.602     ± 54.681  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      55060.360    ± 471.163  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65981.782   ± 1174.186  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63828.282    ± 373.375  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10202.779    ± 523.538  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10545.919    ± 111.192  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10243.253    ± 220.559  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        859.995     ± 24.270  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        687.264     ± 24.248  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7317.506     ± 84.763  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5065.670    ± 310.217  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6817.494    ± 110.338  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     680948.047  ± 19448.635  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     710215.280  ± 80739.824  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     752342.722  ± 65894.417  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     704073.410  ± 29999.304  ops/s
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
