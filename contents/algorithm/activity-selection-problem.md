# Activity Selection Problem

A document about selecting as many non-conflicting activities within a given time frame.

## Method

Given a list of activities each consisting of a start and finish time, sort in increasing order of finish times. Special cases where the start time equals the finish time should be given less precedence. This can be accomplished by sorting activities with equal finish time by increasing order of start times. Then add the activity with earliest finish time into a new list of selected activities. Finally, for each subsequent activity, add it into the list of selected activities if its start time is later than the finish time of the last selected activity.

## Implementation

Python implementation of activity selection problem.

```python
from operator import itemgetter

def get_selected_activities(data):
    # data = [(0, 1), (1, 1), (2, 3), (2, 4)]
    if len(data) < 1:
        return []
    data.sort(key=itemgetter(1, 0))
    selected = [data[0]]
    for i in range(1, len(data)):
        if data[i][0] >= selected[-1][1]:
            selected.append(data[i])
    return selected

```

## References

1. <https://en.wikipedia.org/wiki/Activity_selection_problem>
