# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-07T08:20:56Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.16K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.45K | ± 1.11K | ops/s | 1.2x slower |
| prometheusAdd | 51.38K | ± 190.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.94K | ± 8.54K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 15.07 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.61K | ± 12.17 | ops/s | 9.9x slower |
| simpleclientAdd | 6.10K | ± 277.66 | ops/s | 11x slower |
| openTelemetryAdd | 1.35K | ± 215.51 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.27K | ± 85.45 | ops/s | 51x slower |
| openTelemetryInc | 1.25K | ± 19.45 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 38.31 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 42.08 | ops/s | 1.2x slower |
| prometheusNative | 2.99K | ± 79.51 | ops/s | 1.7x slower |
| openTelemetryClassic | 690.57 | ± 3.51 | ops/s | 7.5x slower |
| openTelemetryExponential | 551.86 | ± 38.84 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 531.88K | ± 6.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 530.92K | ± 9.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 510.32K | ± 8.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.77K | ± 6.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44942.906   ± 8535.106  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1345.957    ± 215.506  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1246.658     ± 19.453  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1269.356     ± 85.450  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51383.850    ± 190.039  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65157.507   ± 1145.707  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55445.042   ± 1114.855  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6101.970    ± 277.663  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6702.181     ± 15.073  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6608.654     ± 12.175  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.565      ± 3.507  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.859     ± 38.839  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5197.485     ± 38.313  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2993.167     ± 79.512  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.805     ± 42.076  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505768.453   ± 6546.679  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     510319.316   ± 8978.314  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     530919.773   ± 9288.963  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531877.194   ± 6263.088  ops/s
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
