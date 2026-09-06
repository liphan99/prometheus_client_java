# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-06T08:11:08Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 253.24 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.61K | ± 1.27K | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 120.00 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.46K | ± 767.70 | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 173.08 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 121.46 | ops/s | 10x slower |
| simpleclientAdd | 6.09K | ± 326.76 | ops/s | 11x slower |
| openTelemetryAdd | 1.55K | ± 261.32 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.40K | ± 216.82 | ops/s | 47x slower |
| openTelemetryInc | 1.26K | ± 26.02 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 98.77 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 52.34 | ops/s | 1.2x slower |
| prometheusNative | 2.87K | ± 65.15 | ops/s | 1.9x slower |
| openTelemetryClassic | 680.79 | ± 26.61 | ops/s | 7.9x slower |
| openTelemetryExponential | 568.47 | ± 31.77 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 533.80K | ± 3.21K | ops/s | **fastest** |
| prometheusWriteToNull | 532.82K | ± 12.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.42K | ± 8.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.40K | ± 4.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47464.057    ± 767.703  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1546.070    ± 261.320  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1255.613     ± 26.019  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1397.418    ± 216.819  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51221.386    ± 119.998  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66074.036    ± 253.237  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55612.560   ± 1272.265  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6087.291    ± 326.763  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6537.437    ± 173.084  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6516.576    ± 121.458  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.787     ± 26.609  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.474     ± 31.769  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5364.556     ± 98.769  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2867.880     ± 65.148  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.909     ± 52.343  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509403.267   ± 4348.046  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516424.697   ± 8907.014  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533797.739   ± 3213.046  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532824.534  ± 12586.705  ops/s
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
