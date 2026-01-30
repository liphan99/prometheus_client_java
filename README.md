# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-01-30T05:27:08Z
- **Commit:** [`8c1cf17`](https://github.com/liphan99/prometheus_client_java/commit/8c1cf1747c382cf80c40e88b7114125976ebd9c4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.69K | ± 148.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 280.60 | ops/s | 1.2x slower |
| prometheusAdd | 51.66K | ± 94.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.52K | ± 1.86K | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 40.68 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.44K | ± 243.48 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 214.17 | ops/s | 10x slower |
| openTelemetryAdd | 1.53K | ± 285.34 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.39K | ± 186.30 | ops/s | 48x slower |
| openTelemetryInc | 1.28K | ± 50.15 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.08K | ± 291.04 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 39.62 | ops/s | 1.1x slower |
| prometheusNative | 3.14K | ± 77.83 | ops/s | 1.6x slower |
| openTelemetryClassic | 665.23 | ± 34.33 | ops/s | 7.6x slower |
| openTelemetryExponential | 509.84 | ± 13.54 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.80K | ± 6.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.87K | ± 3.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.49K | ± 6.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.22K | ± 6.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49520.292   ± 1864.813  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1525.173    ± 285.341  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1276.762     ± 50.152  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1390.300    ± 186.300  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51657.584     ± 94.696  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66687.369    ± 148.047  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57053.460    ± 280.604  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6427.367    ± 214.172  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6759.562     ± 40.675  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6436.878    ± 243.485  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.230     ± 34.330  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        509.837     ± 13.540  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5076.314    ± 291.043  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3143.222     ± 77.826  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4535.181     ± 39.615  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526487.837   ± 6674.945  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522215.095   ± 6572.296  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540871.848   ± 3115.959  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548804.331   ± 6395.844  ops/s
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
