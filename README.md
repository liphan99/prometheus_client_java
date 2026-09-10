# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-10T08:20:45Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.77K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.42K | ± 728.20 | ops/s | 1.1x slower |
| prometheusAdd | 51.09K | ± 587.32 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.44K | ± 1.55K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 182.88 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 124.91 | ops/s | 10.0x slower |
| simpleclientAdd | 6.12K | ± 291.23 | ops/s | 11x slower |
| openTelemetryAdd | 1.38K | ± 232.89 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.28K | ± 160.41 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 14.98 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 9.50 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 35.40 | ops/s | 1.2x slower |
| prometheusNative | 2.98K | ± 134.34 | ops/s | 1.8x slower |
| openTelemetryClassic | 691.46 | ± 33.46 | ops/s | 7.6x slower |
| openTelemetryExponential | 575.68 | ± 21.31 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 529.94K | ± 4.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.02K | ± 7.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 503.02K | ± 5.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 499.35K | ± 5.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48442.781   ± 1551.993  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1382.971    ± 232.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1249.337     ± 14.985  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1284.700    ± 160.415  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51089.800    ± 587.316  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64769.676   ± 1413.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56421.042    ± 728.198  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6120.092    ± 291.229  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.364    ± 182.879  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6490.831    ± 124.908  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.458     ± 33.456  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.680     ± 21.305  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5225.143      ± 9.504  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2980.572    ± 134.341  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4458.481     ± 35.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499351.061   ± 5457.666  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     503017.505   ± 5230.300  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524015.172   ± 7228.687  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     529936.478   ± 4256.625  ops/s
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
