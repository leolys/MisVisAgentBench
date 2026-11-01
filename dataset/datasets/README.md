# Datasets

This directory contains a **partial release** of MisVisAgentBench. The **full dataset will be released here in a future update**.

The current release contains 10 task pairs and 20 chart instances across four domains and three chart types. Nine tasks include numerical reference tables; `demo_006` provides chart images only. Results on this subset should not be presented as full-benchmark results.

| File or folder | Contents |
| --- | --- |
| [tasks.jsonl](tasks.jsonl) | Task instructions, context, available actions and paired chart paths |
| [annotations.json](annotations.json) | Reference answers, explanations and task metadata |
| [manifest.json](manifest.json) | Dataset version, conditions and task list |
| [samples/](samples/) | Clean and misleading charts, with numerical tables where available |

Provide the task record and one chart condition to the evaluated system. Keep answer annotations and numerical reference tables on the evaluator side.

See [data format](../../docs/DATA_FORMAT.md) and [metric definitions](../../docs/METRICS.md) for usage details.
