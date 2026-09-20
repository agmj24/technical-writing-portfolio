```troff
.TH VTK-CHECK 1 "March 2026" "vtk 4.2" "vtk Command Reference"
.SH NAME
vtk-check \- run a structural check against a design file
.SH SYNOPSIS
.B vtk check
[\fB\-file\fR \fI<design_file>\fR]
[\fB\-rules\fR \fI<ruleset>\fR]
[\fB\-severity\fR \fI<level>\fR]
[\fB\-report\fR \fI<output_file>\fR]
.SH DESCRIPTION
Runs a rule-based structural check against a design file and reports any violations found.
.SS Data Types
.TP
\fI<design_file>\fR
String. A file path.
.TP
\fI<ruleset>\fR
String. One of: standard, strict, custom.
.TP
\fI<level>\fR
String. One of: info, warning, error.
.TP
\fI<output_file>\fR
String. A file path.
.SH ARGUMENTS
.TP
\fB\-file\fR \fI<design_file>\fR
Mandatory. Path to the design file to check.
.TP
\fB\-rules\fR \fI<ruleset>\fR
Optional. Rule set to apply. Defaults to
.BR standard .
.TP
\fB\-severity\fR \fI<level>\fR
Optional. Minimum severity to report. Defaults to
.BR warning .
.TP
\fB\-report\fR \fI<output_file>\fR
Optional. Writes results to a file instead of the terminal.
.SH EXAMPLES
.EX
vtk check \-file top_module.def \-rules strict \-severity error \-report results.log
.EE
.SH SEE ALSO
.BR vtk-explain (1),
.BR vtk-rules-list (1)
```troff
