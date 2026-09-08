# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-08T08:15:02Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.63K | ± 542.60 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.23K | ± 563.01 | ops/s | 1.1x slower |
| prometheusAdd | 48.09K | ± 523.04 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.40K | ± 449.49 | ops/s | 1.3x slower |
| simpleclientInc | 6.32K | ± 32.19 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.02K | ± 196.40 | ops/s | 9.7x slower |
| simpleclientAdd | 5.92K | ± 135.89 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.40K | ± 131.29 | ops/s | 42x slower |
| openTelemetryInc | 1.39K | ± 68.31 | ops/s | 42x slower |
| openTelemetryAdd | 1.35K | ± 105.95 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 404.63 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 41.75 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 83.34 | ops/s | 1.6x slower |
| openTelemetryClassic | 597.49 | ± 13.56 | ops/s | 8.5x slower |
| openTelemetryExponential | 509.44 | ± 8.43 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 624.02K | ± 1.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 609.19K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 594.34K | ± 1.83K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 576.64K | ± 1.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44396.318    ± 449.488  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1352.999    ± 105.954  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1391.947     ± 68.313  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1402.869    ± 131.286  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48093.112    ± 523.042  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58634.317    ± 542.600  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51232.557    ± 563.014  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5921.110    ± 135.894  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6319.693     ± 32.187  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6019.858    ± 196.403  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        597.493     ± 13.561  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        509.436      ± 8.425  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5059.660    ± 404.628  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3131.778     ± 83.343  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4354.204     ± 41.745  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     576644.572   ± 1547.868  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     594343.509   ± 1831.105  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     609190.578   ± 6128.382  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     624017.229   ± 1121.007  ops/s
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
