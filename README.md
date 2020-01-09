# skelevision
An implementation of the Log-Skeleton Visualiser in python.

## Installation
As the package isn't at the moment on pypi, we recommend installing it by cloning this repository, and from the root of it run the following command:
```shell 
pip install -e .
```

## Development
Make sure to first install all dependencies via:
```shell
pip install -r requirements.txt
```

### Testing
You can run the following command from the root directory to start the test suit:
```shell
pytest
```
### Documentation
 skelevision package — skelevision documentation         

### Navigation

*   [index](genindex.html "General Index")
*   [modules](py-modindex.html "Python Module Index") |
*   [skelevision documentation](index.html) »

skelevision package[¶](#skelevision-package "Permalink to this headline")
=========================================================================

Submodules[¶](#submodules "Permalink to this headline")
-------------------------------------------------------

skelevision.exceptions module[¶](#module-skelevision.exceptions "Permalink to this headline")
---------------------------------------------------------------------------------------------

_exception_ `skelevision.exceptions.``IllegalLogAction`[¶](#skelevision.exceptions.IllegalLogAction "Permalink to this definition")

Bases: `Exception`

Raised when an incorrect action is performed on a log (e.g. in a trace-to-frequency log import duplicated traces)

skelevision.miners module[¶](#module-skelevision.miners "Permalink to this headline")
-------------------------------------------------------------------------------------

_class_ `skelevision.miners.``LogSkeleton`[¶](#skelevision.miners.LogSkeleton "Permalink to this definition")

Bases: [`skelevision.miners.Miner`](#skelevision.miners.Miner "skelevision.miners.Miner")

Representation of the mine method Works like a base python dict, where the keys are string denoting relationships and statistics and the values are dictionaries representing the relationships and statistics of individual activities.

`load`()[¶](#skelevision.miners.LogSkeleton.load "Permalink to this definition")

_static_ `mine`(_log_, _reqA_, _forbA_)[¶](#skelevision.miners.LogSkeleton.mine "Permalink to this definition")

Returns a dictionary, containing the relationships and statistics.

Parameters

*   **log** (TraceLog) – tracelog object
    
*   **reqA** (set()) – If one or more of the selected activities does not occur in a trace, the entire trace will be filtered out.
    
*   **forbA** (set()) – If one or more of the selected activities occurs in a trace, the entire trace will be filtered out.
    

Returns

the pairs of the activities which are never together in any of the traces

Return type

set of tuples

`save`()[¶](#skelevision.miners.LogSkeleton.save "Permalink to this definition")

_class_ `skelevision.miners.``Miner`[¶](#skelevision.miners.Miner "Permalink to this definition")

Bases: `abc.ABC`

_abstract_ `load`()[¶](#skelevision.miners.Miner.load "Permalink to this definition")

_abstract_ `mine`(_log_)[¶](#skelevision.miners.Miner.mine "Permalink to this definition")

_abstract_ `save`()[¶](#skelevision.miners.Miner.save "Permalink to this definition")

skelevision.objects module[¶](#module-skelevision.objects "Permalink to this headline")
---------------------------------------------------------------------------------------

_class_ `skelevision.objects.``TraceLog`(_\*args_, _\*\*kwargs_)[¶](#skelevision.objects.TraceLog "Permalink to this definition")

Bases: `collections.abc.MutableMapping`

Representation of a trace log. Works like a base python dict, where the keys are tuples denoting individual traces (e.g. ‘(“a”, “b”, “c”)’ denoted trace ‘abc’) and the values denote the frequencies of the traces.

_static_ `activity_2_freq`(_trace_)[¶](#skelevision.objects.TraceLog.activity_2_freq "Permalink to this definition")

For a given trace, return a mapping from activity to frequency in trace.

Parameters

**trace** (tuple of str) – a trace as a tuple of activities

Returns

mapping from activity to frequency in trace

Return type

dict

`always_after`()[¶](#skelevision.objects.TraceLog.always_after "Permalink to this definition")

Returns a set of tuples, representing the pairs of the activities which after any occurrence of the first activity the second activity always occurs.

Returns

pairs of the activities which after any occurrence of the first activity the second activity always occurs.

Return type

set\`\`of \`tuples

`always_before`()[¶](#skelevision.objects.TraceLog.always_before "Permalink to this definition")

Returns a set of tuples, representing the pairs of the activities which before any occurrence of the first activity the second activity always occurs.

Returns

pairs of the activities which before any occurrence of the first activity the second activity always occurs.

Return type

set\`\`of \`tuples

`augment`(_start='\[>'_, _end='\[\]'_)[¶](#skelevision.objects.TraceLog.augment "Permalink to this definition")

Returns a similar TraceLog object where each trace contains an aditional start and end activity.

`equivalence`()[¶](#skelevision.objects.TraceLog.equivalence "Permalink to this definition")

Returns a set of tuples, representing the pairs of the activities which are always together in all of the traces the same number of times.

Returns

the pairs of the activities which are always together in all of the traces the same number of times

Return type

set\`\`of \`tuples

`filter_traces`(_reqA=None_, _forbA=None_)[¶](#skelevision.objects.TraceLog.filter_traces "Permalink to this definition")

Filters the tracelog based on required and forbidden activities.

Parameters

*   **reqA** (set()) – If one or more of the selected activities does not occur in a trace, the entire trace will be filtered out.
    
*   **forbA** (set()) – If one or more of the selected activities occurs in a trace, the entire trace will be filtered out.
    

Returns

Mapping from activity to coresponding event list.

Return type

TraceLog

`follows`(_distance=1_)[¶](#skelevision.objects.TraceLog.follows "Permalink to this definition")

Returns a mapping (aka. dict) from pairs of activities to frequency. A pair (a, b) is part of the mapping if activity b follows activity a, at a certain distance, in any of the traces.

Parameters

**distance** (_int_) – Distance two activities have to be appart to be counted in the mapping.

_static_ `freq_2_activities`(_trace_)[¶](#skelevision.objects.TraceLog.freq_2_activities "Permalink to this definition")

For a given trace, return a mapping from frequency to set of activities, with that frequency in the trace.

Parameters

**trace** (tuple of str) – a trace as a tuple of activities

Returns

mapping from frequency to set activities in trace

Return type

dict

_static_ `from_txt`(_filepath_, _delimiter=None_, _frequency\_idx=0_, _first\_activity\_idx=2_)[¶](#skelevision.objects.TraceLog.from_txt "Permalink to this definition")

Parses a .txt file containing a trace log and returns a TraceLog object of it.

Parameters

*   **filepath** (_path-like_) – The path to the .txt file.
    
*   **delimiter** (str) – Character delimiting the different values. Default None, thus splitting by all the whitespace.
    
*   **frequency\_idx** (int) – Default 0.
    
*   **first\_activity\_idx** (int) – Default 2.
    

Returns

Mapping from activity to coresponding event list.

Return type

TraceLog

_static_ `from_xes`(_filepath_)[¶](#skelevision.objects.TraceLog.from_xes "Permalink to this definition")

Parses a .xes or a .gz file containing a trace log and returns a TraceLog object of it.

Parameters

**filepath** (_path-like_) – The path to the .xes or .gz file.

Returns

Mapping from activity to coresponding event list.

Return type

TraceLog

_property_ `labels`[¶](#skelevision.objects.TraceLog.labels "Permalink to this definition")

Returns all the unique labels of activities in the trace log.

`max_counter`()[¶](#skelevision.objects.TraceLog.max_counter "Permalink to this definition")

Returns a dict, representing a Mapping from activity to the max amount of times the activity appears in any trace of the TraceLog.

> Parameters

activity: ‘str’

the name of the activity

Returns

Mapping from activity to the max amount of times the activity appears in any trace of the TraceLog.

Return type

‘dict’

`min_counter`()[¶](#skelevision.objects.TraceLog.min_counter "Permalink to this definition")

Returns a dict, representing a Mapping from activity to the min amount of times the activity appears in any trace of the TraceLog.

> Parameters

activity: ‘str’

the name of the activity

Returns

Mapping from activity to the min amount of times the activity appears in any trace of the TraceLog.

Return type

‘dict’

`never_together`()[¶](#skelevision.objects.TraceLog.never_together "Permalink to this definition")

Returns a set of tuples, representing the pairs of the activities which are never together in any of the traces.

Returns

the pairs of the activities which are never together in any of the traces

Return type

set of tuples

`save_to_file`(_filepath_, _format='txt'_)[¶](#skelevision.objects.TraceLog.save_to_file "Permalink to this definition")

Save a TraceLog object as a .txt file.

`statistics`()[¶](#skelevision.objects.TraceLog.statistics "Permalink to this definition")

`sum_counter`()[¶](#skelevision.objects.TraceLog.sum_counter "Permalink to this definition")

Returns a dict, representing a Mapping from activity to the amount of times the activity appears in the TraceLog.

> Parameters

activity: ‘str’

the name of the activity

Returns

Mapping from activity to the amount of times the activity appears in the TraceLog.

Return type

‘dict’

skelevision.utils module[¶](#module-skelevision.utils "Permalink to this headline")
-----------------------------------------------------------------------------------

`skelevision.utils.``follows`(_trace_, _distance=1_)[¶](#skelevision.utils.follows "Permalink to this definition")

`skelevision.utils.``predecessors`(_trace_)[¶](#skelevision.utils.predecessors "Permalink to this definition")

`skelevision.utils.``successors`(_trace_)[¶](#skelevision.utils.successors "Permalink to this definition")

Module contents[¶](#module-skelevision "Permalink to this headline")
--------------------------------------------------------------------

### [Table of Contents](index.html)

*   [skelevision package](#)
    *   [Submodules](#submodules)
    *   [skelevision.exceptions module](#module-skelevision.exceptions)
    *   [skelevision.miners module](#module-skelevision.miners)
    *   [skelevision.objects module](#module-skelevision.objects)
    *   [skelevision.utils module](#module-skelevision.utils)
    *   [Module contents](#module-skelevision)

### This Page

*   [Show Source](_sources/skelevision.rst.txt)

### Quick search

 

$('#searchbox').show(0);

### Navigation

*   [index](genindex.html "General Index")
*   [modules](py-modindex.html "Python Module Index") |
*   [skelevision documentation](index.html) »

© Copyright 2020, nowraj. Created using [Sphinx](http://sphinx-doc.org/) 2.2.1.
