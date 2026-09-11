# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T08:19:55Z
- **Commit:** [`8c1cf17`](https://github.com/liphanho/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 30.58K | ± 418.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.34K | ± 185.77 | ops/s | 1.0x slower |
| prometheusInc | 30.00K | ± 444.54 | ops/s | 1.0x slower |
| prometheusAdd | 28.53K | ± 1.14K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.60K | ± 92.48 | ops/s | 4.0x slower |
| simpleclientInc | 7.47K | ± 71.02 | ops/s | 4.1x slower |
| simpleclientAdd | 7.28K | ± 130.11 | ops/s | 4.2x slower |
| openTelemetryInc | 1.24K | ± 46.63 | ops/s | 25x slower |
| openTelemetryAdd | 1.14K | ± 101.80 | ops/s | 27x slower |
| openTelemetryIncNoLabels | 1.09K | ± 87.93 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.91K | ± 51.10 | ops/s | **fastest** |
| prometheusClassic | 2.66K | ± 232.59 | ops/s | 1.8x slower |
| prometheusNative | 2.19K | ± 21.71 | ops/s | 2.2x slower |
| openTelemetryClassic | 389.84 | ± 18.92 | ops/s | 13x slower |
| openTelemetryExponential | 340.14 | ± 17.20 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 330.12K | ± 4.18K | ops/s | **fastest** |
| prometheusWriteToNull | 324.94K | ± 2.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 312.56K | ± 9.02K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 302.13K | ± 8.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30579.023    ± 418.945  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1140.257    ± 101.804  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.687     ± 46.627  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1089.441     ± 87.926  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28534.856   ± 1143.126  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29996.720    ± 444.537  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30337.789    ± 185.768  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7280.091    ± 130.111  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7467.489     ± 71.023  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7599.577     ± 92.484  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        389.844     ± 18.922  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        340.143     ± 17.201  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2657.704    ± 232.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2193.541     ± 21.706  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4905.450     ± 51.098  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     312562.014   ± 9020.496  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     302129.054   ± 8244.239  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     330117.225   ± 4181.796  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     324936.806   ± 2875.214  ops/s
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
