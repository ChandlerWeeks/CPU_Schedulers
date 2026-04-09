# CPU Scheduling Simulator

This project is a small Python notebook that simulates common CPU scheduling algorithms from a CSV input file and visualizes the result as a Gantt chart. It also computes per-process and average scheduling metrics such as response time, waiting time, and turnaround time.

The simulator is implemented in [`cpu_scheduler.ipynb`](/Users/chandler/Desktop/CPU%20Simulator/cpu_scheduler.ipynb) and uses [`processes.csv`](/Users/chandler/Desktop/CPU%20Simulator/processes.csv) as its input dataset.

## Features

- Loads process data from CSV
- Simulates 7 scheduling strategies
- Draws a Gantt chart with process execution over time
- Exports the chart as a PNG image
- Computes:
  - Response time
  - Waiting time
  - Turnaround time

## Supported Algorithms

The notebook supports the following scheduling modes:

| Key | Algorithm | Implementation Mode |
| --- | --- | --- |
| `FCFS` | First Come First Served | Non-preemptive |
| `SJF` | Shortest Job First | Non-preemptive |
| `SRTF` | Shortest Remaining Time First | Preemptive |
| `RR` | Round Robin | Time-sliced |
| `PRIORITY` | Priority Scheduling | Non-preemptive |
| `PRIORITY_P` | Priority Scheduling | Preemptive |
| `MLQ` | Multilevel Queue | `Q0 = FCFS`, `Q1 = RR`, `Q2 = FCFS` |

## Project Structure

- [`cpu_scheduler.ipynb`](/Users/chandler/Desktop/CPU%20Simulator/cpu_scheduler.ipynb): main simulator notebook
- [`processes.csv`](/Users/chandler/Desktop/CPU%20Simulator/processes.csv): sample process dataset
- [`README.md`](/Users/chandler/Desktop/CPU%20Simulator/README.md): project documentation

## Input Format

The simulator expects a CSV file with these columns:

| Column | Description |
| --- | --- |
| `pid` | Process ID |
| `arrival_time` | Time the process enters the ready queue |
| `burst_time` | CPU time required by the process |
| `priority` | Priority value, where a lower number means higher priority |
| `queue_level` | Queue index used only by the multilevel queue algorithm |

Example:

```csv
pid,arrival_time,burst_time,priority,queue_level
P1,0,8,3,1
P2,1,4,1,0
P3,2,9,4,2
```

## Requirements

Use Python 3 with the following packages:

- `jupyter`
- `pandas`
- `matplotlib`
- `numpy`
- `ipython`

## Setup

Create a virtual environment and install dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install jupyter pandas matplotlib numpy ipython
```

Then start Jupyter:

```bash
jupyter notebook cpu_scheduler.ipynb
```

## How To Use

1. Open [`cpu_scheduler.ipynb`](/Users/chandler/Desktop/CPU%20Simulator/cpu_scheduler.ipynb).
2. Make sure [`processes.csv`](/Users/chandler/Desktop/CPU%20Simulator/processes.csv) contains the processes you want to simulate.
3. In the configuration cell, set:
   - `ALGORITHM` to one of the supported algorithm keys
   - `QUANTUM` for `RR` or `MLQ`
4. Run all notebook cells.
5. Review the generated Gantt chart and statistics table.

The configuration cell currently uses this pattern:

```python
ALGORITHM = 'PRIORITY'
QUANTUM = 3
```

## Output

When the notebook runs, it:

- Displays the loaded process table
- Runs the selected scheduling algorithm
- Shows a Gantt chart in the notebook
- Saves the chart to a PNG file named like `gantt_<algorithm>.png`
- Displays a table of per-process metrics
- Prints average response, waiting, and turnaround times

## Notes

- `priority`: smaller number means higher priority
- `queue_level`: `0` is highest and `2` is lowest
- `queue_level` is only used by the `MLQ` scheduler
- The multilevel queue implementation gives strict preference to higher-priority queues

## Educational Purpose

This project is useful for learning and demonstrating how different CPU scheduling policies affect execution order and scheduling performance metrics.
