# Summary

Fabric needs a flexible datepicker component

# Motivation

The resulting datepicker should
- be flexible enough to support minor UI deviations (e.g. 'I want to highlight 5 days each month instead of (or in addition to) disabling unavailable days')
- support the most basic/common set of usecases - possibly with a marginally more painful API if it supports compostion as described below
- provide a way for more advanced usecases to _eject_ from the core supported usecase, but not need to be written from scratch (e.g. a Day or Month component could possibly be reused, or some logic we expose)
  - this follows the Fabric 'building block' approach, and the approach taken with fClickable and fDeadToggle thus far

It should _not_ support all usecases, certain datepicker or calendar needs may require that FINN/Fabric standardizes on a module (such as `fullcalendar`)

# Implementation

Supported:
- Single date
- Two-date-range
- Disabled days via function
- Arbitrary classes on dates via function (ability to change date UI if the core functionality is the same)
- Show/hide sibling months (e.g. show the 1st of next month if it's on a Sunday from the current month)

Excluded:
- Any kind of multiple-ranges (e.g. showing multiple all-day range appointments like Google Calendar in month view)
- Text on a range
- Any kind of drag-and-drop
- Tightly coupled behavior on dates/datepicker with popups/inputs/etc.
  - The core Month or Calendar should just emit an event, it's up to the implementation to figure out what to do with that - not manage behaviors for the user
  - Fabric could possibly provide better support for a core set of behaviors by providing logic or wrapper-components, etc
