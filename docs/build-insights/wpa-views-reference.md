---
title: "C++ Build Insights: Windows Performance Analyzer views reference"
description: "Reference for C++ Build Insights views available in Windows Performance Analyzer."
ms.date: "09/16/2019"
helpviewer_keywords: ["C++ Build Insights", "throughput analysis", "build time analysis", "vcperf.exe"]
ms.assetid: ceb8e00f-5e98-4948-bd2c-1ac3880b96d4
---
# C++ Build Insights: Windows Performance Analyzer views reference

## Introduction

This section provides details on each of the C++ Build Insights views available in Windows Performance Analyzer (WPA). Use this page to find:

- data column descriptions; and
- available presets for each view, including their intended use and preferred viewing mode.

If you are new to WPA, we recommend that you first familiarize yourself with the [basics of WPA for C++ Build Insights](wpa-basics.md).

## Build Explorer

The Build Explorer view is used to:

- diagnose parallelism issues;
- determine if your build time is dominated by parsing, code generation, or linking; and
- identify bottlenecks and long poles.

### Build Explorer view data columns

| Column Name              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BuildTimelineDescription | A textual description the timeline on which the current activity or property is occurring.                                                                                                                                                                                                                                                                                                                                                                                                           |
| BuildTimelineId          | A zero-based identifier for the timeline on which the current activity or property is occurring.                                                                                                                                                                                                                                                                                                                                                                                                     |
| Component                | The component that was being compiled or linked when the current event was emitted. The value of this column is *\<Invocation X Info\>* when no component is associated with this event. X is a unique numerical identifier for the invocation that was being executed at the time the event was emitted. This identifier is the same as the one in the InvocationId column for this event.                                                                                                          |
| Count                    | The number of activities or properties represented by this data row. This value is always 1 and is only useful in aggregation scenarios when multiple rows are grouped.                                                                                                                                                                                                                                                                                                                              |
| ExclusiveCPUTime         | The amount of CPU time in milliseconds that was allocated to this activity. The time that was spent in children activities is not included in this amount.                                                                                                                                                                                                                                                                                                                                           |
| ExclusiveDuration        | The millisecond duration of the activity. The duration of children activities is not included in this amount.                                                                                                                                                                                                                                                                                                                                                                                        |
| InclusiveCPUTime         | The amount of CPU time in milliseconds that was allocating to this activity and all children activities.                                                                                                                                                                                                                                                                                                                                                                                             |
| InclusiveDuration        | The millisecond duration of this activity, including all children activities.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| InvocationDescription    | A textual description of the invocation during which this event occurred. The description includes whether it was *cl.exe* or *link.exe*, a unique numerical invocation identifier, and, if applicable, the full path to the component that was being compiled or linked during the invocation. For invocations that don't build any component, or for the ones that build multiple components, the path is left blank. The invocation identifier is the same as the one in the InvocationId column. |
| InvocationId             | A unique numerical identifier for the invocation during which this event occurred.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Name                     | The name of the activity or property represented by this event.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Time                     | A timestamp identifying the time at which the event occurred.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Tool                     | The tool that was executing when this event occurred. The value of this column is either CL or Link.                                                                                                                                                                                                                                                                                                                                                                                                 |
| Type                     | The type of the current event. This value is either Activity or Property.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Value                    | If the current event is a property, this column contains its value. This column is left blank when the current event is an activity.                                                                                                                                                                                                                                                                                                                                                                 |

### Build Explorer view presets

| Preset Name           | Preferred View Mode | How to Use                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Activity Statistics   | Graph / Table       | Use this preset to view aggregated statistics for all Build Explorer activities. In table mode, determine at a glance if your build is dominated by parsing, code generation, or the linker by looking at the aggregated durations for each activity sorted in descending order. Drill in by expanding the top node to easily find which invocations take the most time for these top activities. Adjust WPA settings to show averages or other types of aggregations if desired. In graph mode, see when each activity is active during your build. |
| Invocations           | Graph               | Scroll down through a list of invocations in the graph view sorted by start time. If desired, use in conjunction with the CPU (Sampled) view to find invocations that align with low CPU utilization zones. Detect parallelism issues.                                                                                                                                                                                                                                                                                                               |
| Invocation Properties | Table               | Quickly find key information about a given compiler or linker invocation. Determine its version, working directory, or the full command line it was invoked with.                                                                                                                                                                                                                                                                                                                                                                                    |
| Timelines             | Graph               | See a bar graph of how your build was parallelized. Identify parallelism issues and bottlenecks at a glance. Configure WPA to assign different meanings to the bars according to your needs. Choose invocation descriptions as the last grouped column to view a color coded bar graph of all your invocations to quickly identify long pole culprits. Then, zoom in and choose the activity name as the last grouped column to see what was the longest parts of these long poles.                                                                  |

## Files

The Files view is used to:

- determine the headers that are the most included; and
- assist in deciding what to include in a pre-compiled header (PCH).

### Files view data columns

| Column Name              | Description                                                                                                                                                                     |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ActivityName             | The activity that was in progress when this file event was emitted. Currently, this value is always *Parsing*.                                                                  |
| BuildTimelineDescription | *                                                                                                                                                                               |
| BuildTimelineId          | *                                                                                                                                                                               |
| Component                | *                                                                                                                                                                               |
| Count                    | *                                                                                                                                                                               |
| Depth                    | The zero-based position in the include tree in which this file is found. Counting starts at the root of the include tree. A value of 0 typically corresponds to a .c/.cpp file. |
| ExclusiveDuration        | *                                                                                                                                                                               |
| IncludedBy               | The full path of the file that included the current file.                                                                                                                       |
| IncludedPath             | The full path of the current file.                                                                                                                                              |
| InclusiveDuration        | *                                                                                                                                                                               |
| InvocationId             | *                                                                                                                                                                               |
| StartTime                | A timestamp that represents the time at which the current file event was emitted.                                                                                               |
| Tool                     | *                                                                                                                                                                               |

\* The value of this column is the same as in the [Build Explorer](#build-explorer-view-data-columns) view.

### Files view presets

| Preset Name | Preferred View Mode | How to Use                                                                                                                                                                                           |
|-------------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Statistics  | Table               | See which files had the highest aggregated parsing time by looking at the list in descending order. Use this information to help you restructure your headers or decide what to include in your PCH. |

## Functions

The Functions view is used to identify long pole functions caused by an excessively long code generation time.

### Functions view data columns

| Column Name              | Description                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------|
| ActivityName             | The activity that was in progress when this function event was emitted. Currently, this value is always *CodeGeneration*. |
| BuildTimelineDescription | *                                                                                                                         |
| BuildTimelineId          | *                                                                                                                         |
| Component                | *                                                                                                                         |
| Count                    | *                                                                                                                         |
| Duration                 | The duration of the code generation activity for this function.                                                           |
| FunctionName             | The name of the function that was undergoing code generation.                                                             |
| InvocationId             | *                                                                                                                         |
| StartTime                | A timestamp that represents the time at which the current function event was emitted.                                     |
| Tool                     | *                                                                                                                         |

\* The value of this column is the same as in the [Build Explorer](#build-explorer-view-data-columns) view.

### Functions view presets

| Preset Name | Preferred View Mode | How to Use                                                                                                                                                                                                                                                                                        |
|-------------|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Statistics  | Table               | See which functions had the highest aggregated code generation time by looking at the list in descending order. Use this information as a hint that your code may contain too many uses of the *__forceinline* keyword, or that some functions may be excessively large.                          |
| Timelines   | Graph               | Look at this bar graph to identify at a glance the location and duration of functions that take the most time to generate. See if they align with bottlenecks in the Build Explorer view. If they do, take appropriate action to reduce their code generation time and benefit your build times.  |