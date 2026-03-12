Continuous Performance Task
----------------------------

The experiment:

In this task participants are required to respond to all letter stimuli except from letter X (by pressing space). This task is based on Conners (2000) Continuous Performance Test.

Qualtrics integration:
----------------------------
To launch this task from a Qualtrics survey, embed the experiment URL in a survey question using the **Open a URL** or **Web Service** feature, passing the participant identifier as a URL parameter.

The experiment reads two URL parameters:

| Parameter     | Description                              | Example value |
|---------------|------------------------------------------|---------------|
| `participant` | Unique identifier for the participant    | `P001`        |
| `session`     | Session number (defaults to `001`)       | `001`         |

**URL format:**

```
https://<your-experiment-host>/continuous_performance_test/?participant=${e://Field/ResponseID}&session=001
```

Replace `<your-experiment-host>` with the domain where the experiment is hosted (e.g. a Pavlovia URL such as `run.pavlovia.org/<username>/continuous_performance_test`).

The Qualtrics piped-text `${e://Field/ResponseID}` automatically inserts the respondent's Qualtrics Response ID as the participant identifier, linking the task data to the survey response.

When the `participant` parameter is present in the URL the experiment starts immediately, skipping the participant-information dialog. When it is absent (e.g. during standalone testing) the dialog is shown so you can enter the participant ID manually.

At the end of the task participants see the message:

> *"This task is finished. You can return to the Qualtrics survey."*

You can redirect them back automatically by adding a **redirect URL** (e.g. via a Qualtrics End-of-Survey redirect) pointing to the next page of your survey.

Analysing your data:
----------------------------
Data files are saved in the `data/` folder of the experiment directory. Each file is named using the pattern:

```
data/{participant}_{experiment_name}_{date}.csv
```

For example: `data/P001_continuous_performance_test_2024-01-19_10h30.csv`

The following output formats are generated automatically by PsychoPy:

| File extension | Contents                                            |
|----------------|-----------------------------------------------------|
| `.csv`         | Wide-format trial-by-trial data (primary data file) |
| `.psydat`      | PsychoPy binary data file                           |
| `.log`         | Timestamped event log                               |

**Key columns in the CSV file:**

| Column              | Description                                                       |
|---------------------|-------------------------------------------------------------------|
| `response.corr`     | Trial outcome — `1` = correct response, `0` = incorrect response |
| `response.rt`       | Reaction time (seconds) for trials where a response was made      |
| `response.duration` | Duration of the key press (seconds)                               |
| `response.keys`     | Key pressed (`space`) or empty if no response was made            |

The experiment presents 90 trials in total (30 unique letter stimuli x 3 repetitions, randomised). The overall accuracy score shown to the participant at the end (e.g. *"You scored 85/90 correct"*) counts both correct responses (pressing space for non-X letters) and correct non-responses (withholding a response for the letter X).

References:
----------------------------
Conners, C.K. & MHS Staff. (Eds.) (2000) Conners' Continuous Performance Test II: Computer Program for Windows Technical Guide and Software Manual. North Tonawanda, NY: Multi-Health Systems.

Original Task by Julia Sadka. Online optimisation by SLM (2022-01-19)
