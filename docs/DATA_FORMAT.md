# Data format

Version: `misvisagentbench-datasets-v1.1.0`. Each task has `clean` and `misleading` chart conditions. Available contents are described in the [dataset README](../dataset/datasets/README.md).

All paths inside the dataset JSON files are relative to `dataset/datasets/`.

## Task records

`tasks.jsonl` contains one JSON object per task pair. The task is shared across conditions; select one entry from `charts` for each run.

| Field | Type | Meaning |
| --- | --- | --- |
| `task_id` | string | Stable sample identifier |
| `title` | string | Business task title |
| `instruction` | string | Task instruction |
| `chart_reference` | string or null | Additional chart-use instruction, when present |
| `context` | array | Read-only business context entries with `label` and `value` |
| `decision_label` | string | Primary decision field label |
| `submit_label` | string | Submission action label |
| `actions` | array | Available actions with `id` and `label` |
| `charts` | object | `clean` and `misleading` chart paths |

Action IDs are `A`, `B` and `C`, scoped to a task. Preserve their order and labels across both conditions. A task ID and action ID together identify a decision.

## Answer annotations

`annotations.json` contains a `version` and a `tasks` object keyed by task ID.

| Field | Meaning |
| --- | --- |
| `correct_action_id` | Correct primary action, shared by both conditions |
| `misleading_action_ids` | Targeted incorrect actions associated with misleading evidence |
| `explanation` | Reference reasoning for the correct answer |
| `domain` | Task domain |
| `chart_type` | Chart category |
| `misleading_mechanism` | Misleading mechanism category |
| `data` | Numerical reference table path, or null when unavailable |

These fields are evaluator metadata. Provide only the task record and one chart condition to the agent. Numerical tables are reference data for inspecting answers and are not agent inputs for chart-only runs.

## Charts and numerical data

`samples/<task_id>/` contains `clean.png`, a misleading chart in PNG or JPEG format, and `data.csv` when available. CSV headers specify the measured quantities; use the units displayed in the corresponding charts. The numerical data are shared by the paired charts.

The scenarios describe benchmark tasks; the numerical tables should not be treated as verified population, health, energy or business statistics.

## Outcomes

For a submitted primary action, use `success` if it equals `correct_action_id`, `misleading_failure` if it matches `misleading_action_ids`, and `irrelevant_action_failure` otherwise. A missing submission is `completion_failure`; execution timeouts and errors use `agent_timeout` and `agent_error`. This outcome vocabulary is consumed by the [metric calculator](METRICS.md).

The release provides primary-decision task data. An external browser integration supplies its own navigation and form execution. For behavioral metrics, record executed steps and primary selections as specified in the metric documentation.

## Dataset manifest

`manifest.json` lists the dataset version, conditions, counts and task IDs.
