# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-12T08:13:01Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 555.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 216.48 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.36K | ± 1.38K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 61.62 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.47K | ± 215.32 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 221.46 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 238.39 | ops/s | 46x slower |
| openTelemetryInc | 1.26K | ± 8.33 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.26K | ± 12.56 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 25.69 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 79.51 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 176.38 | ops/s | 1.8x slower |
| openTelemetryClassic | 671.26 | ± 20.49 | ops/s | 7.8x slower |
| openTelemetryExponential | 556.07 | ± 31.43 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.60K | ± 9.99K | ops/s | **fastest** |
| openMetricsWriteToNull | 521.49K | ± 13.16K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 517.26K | ± 9.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.77K | ± 13.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49356.913   ± 1379.511  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1426.892    ± 238.392  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.822      ± 8.328  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1256.712     ± 12.559  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51454.010    ± 216.477  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65333.657   ± 1228.098  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56728.885    ± 555.041  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.716    ± 221.458  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6624.438     ± 61.623  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6465.079    ± 215.322  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.259     ± 20.493  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.069     ± 31.427  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5248.360     ± 25.692  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.721    ± 176.385  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4373.190     ± 79.513  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510770.170  ± 13734.364  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521486.402  ± 13159.430  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517257.266   ± 9013.658  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535600.720   ± 9994.372  ops/s
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
