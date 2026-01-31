# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-01-31T05:23:38Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.12K | ± 849.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.80K | ± 1.14K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.05K | ± 1.24K | ops/s | 1.0x slower |
| prometheusAdd | 26.75K | ± 1.68K | ops/s | 1.2x slower |
| simpleclientInc | 7.21K | ± 107.78 | ops/s | 4.3x slower |
| simpleclientNoLabelsInc | 6.97K | ± 277.22 | ops/s | 4.5x slower |
| simpleclientAdd | 6.85K | ± 76.93 | ops/s | 4.5x slower |
| openTelemetryIncNoLabels | 1.49K | ± 169.58 | ops/s | 21x slower |
| openTelemetryInc | 1.36K | ± 42.39 | ops/s | 23x slower |
| openTelemetryAdd | 1.22K | ± 89.08 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 69.38 | ops/s | **fastest** |
| prometheusClassic | 3.20K | ± 503.22 | ops/s | 1.4x slower |
| prometheusNative | 2.11K | ± 226.21 | ops/s | 2.2x slower |
| openTelemetryClassic | 503.57 | ± 14.04 | ops/s | 9.0x slower |
| openTelemetryExponential | 381.78 | ± 11.23 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 343.41K | ± 900.96 | ops/s | **fastest** |
| prometheusWriteToByteArray | 339.64K | ± 3.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 314.82K | ± 1.05K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 313.22K | ± 945.58 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30046.906   ± 1241.893  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1215.341     ± 89.080  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1359.148     ± 42.391  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1491.335    ± 169.578  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26747.358   ± 1682.803  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31116.378    ± 849.517  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30803.062   ± 1136.681  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6846.842     ± 76.928  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7205.198    ± 107.781  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6974.743    ± 277.224  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        503.574     ± 14.036  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        381.784     ± 11.231  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3197.814    ± 503.219  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2109.836    ± 226.212  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4539.133     ± 69.376  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     313217.941    ± 945.579  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     314818.420   ± 1050.163  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     339640.272   ± 3248.311  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     343411.417    ± 900.963  ops/s
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
