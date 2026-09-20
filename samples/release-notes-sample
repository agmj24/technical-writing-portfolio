# Tool Name  
**Version V-2026.06**  
June 2026

---

© 2026. All rights reserved.  
This document is protected by copyright. Unauthorized reproduction or distribution is prohibited.

---

## About This Document

This Release Notes document includes the following sections to help you understand the changes in this release of **Tool Name**:

- New Features and Enhancements  
- Known Issues  
- Resolved Bugs  

---

## New Features and Enhancements

The product includes the following new features and enhancements in this release:

- Added `SUPPORT_HIERARCHY` keyword  
- Enhanced `REPORT_FORMAT` keyword  

### Added SUPPORT_HIERARCHY Keyword

Starting with this release, a new keyword **SUPPORT_HIERARCHY** has been added.  

This keyword enables hierarchical analysis of design structures during structural checks. When specified, the tool traverses the design hierarchy and applies rule checks at each level, providing more granular violation reporting.

**Example usage:**

```tcl
SUPPORT_HIERARCHY true
```
### Enhanced REPORT_FORMAT Keyword

Starting with this release, the `REPORT_FORMAT` keyword has been enhanced.
Previously limited to plain text and CSV, the keyword now supports additional output formats: **JSON** and **YAML**. This improvement allows easier integration with external reporting and analytics tools.

**Example usage:**
```tcl
REPORT_FORMAT json
```

---

## Known Issues
The following are the known issues in this release of VTran:

| Issue ID | Description | Workaround |
| --- | --- | --- |
| KI-001 | Hierarchical checks may report duplicate violations when the same module is instantiated multiple times at different levels. | Apply the `UNIQUE_INSTANCE` filter or run checks on flattened designs. |
| KI-002 | When using `REPORT_FORMAT yaml`, very large reports (>50 MB) may cause increased memory usage. | Split the design into smaller blocks or use CSV format for large runs. |
| KI-003 | The new `SUPPORT_HIERARCHY` keyword is currently ignored when the design contains encrypted IP blocks. | Decrypt IP blocks before running hierarchical checks, or exclude them using exclusion rules. |

---

## Resolved Bugs
The following bugs have been resolved in this release:

| Customer ID | Description |
| --- | --- |
| CUST-4821 | Fixed a crash that occurred when the design file contained mixed-case instance names and the `STRICT` ruleset was applied. |
| CUST-4907 | Corrected incorrect severity mapping: violations that should have been reported as error were previously reported as warning when using the standard ruleset. |
| CUST-5012 | Resolved an issue where the `-report` option failed to write output when the target directory did not exist. The tool now creates the directory if permissions allow. |
| CUST-5128 | Fixed incomplete reporting of violations located inside generate blocks.

---
