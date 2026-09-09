# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-09T08:24:11Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.20K | ± 1.45K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.79K | ± 1.14K | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 442.97 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.44K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 62.69 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.33K | ± 245.27 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 214.44 | ops/s | 10x slower |
| openTelemetryAdd | 1.51K | ± 252.62 | ops/s | 43x slower |
| openTelemetryInc | 1.34K | ± 97.10 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.33K | ± 145.70 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 62.34 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 67.98 | ops/s | 1.2x slower |
| prometheusNative | 3.11K | ± 49.43 | ops/s | 1.7x slower |
| openTelemetryClassic | 649.45 | ± 22.14 | ops/s | 8.3x slower |
| openTelemetryExponential | 543.74 | ± 1.37 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 533.32K | ± 4.54K | ops/s | **fastest** |
| prometheusWriteToNull | 527.92K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.19K | ± 8.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.57K | ± 4.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48443.946   ± 1496.411  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1511.634    ± 252.623  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1336.120     ± 97.099  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1329.154    ± 145.696  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51212.785    ± 442.971  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65197.678   ± 1446.554  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55786.037   ± 1142.125  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6298.200    ± 214.439  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.944     ± 62.693  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6333.222    ± 245.267  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        649.449     ± 22.139  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.736      ± 1.366  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5415.260     ± 62.339  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3106.534     ± 49.432  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.856     ± 67.980  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508566.588   ± 4061.905  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514190.138   ± 8371.681  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533317.793   ± 4535.180  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527924.090   ± 2120.124  ops/s
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
