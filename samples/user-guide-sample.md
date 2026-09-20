# VTran Design Check Tool — User Guide

**Document ID:** UG-VT-001  
**Version:** 1.0  
**Status:** Portfolio Sample  
**Last Updated:** June 2026  

---

## Contents

1. [Introduction](#1-introduction)  
2. [Overview](#2-overview)  
3. [Getting Started](#3-getting-started)  
4. [Running a Design Check](#4-running-a-design-check)  
5. [Reviewing Results](#5-reviewing-results)  
6. [Generating a Report](#6-generating-a-report)  
7. [Troubleshooting](#7-troubleshooting)  
8. [Related Documentation](#8-related-documentation)  

---

## 1. Introduction

VTran is a design-check tool that helps engineers identify structural issues in design files before they are released for downstream implementation.

This guide describes how to prepare a design, run a design check, review the results, and generate a report.

---

## 2. Overview

A typical design-check workflow consists of these steps:

1. Prepare the design file  
2. Create a check job  
3. Select a ruleset  
4. Run the check  
5. Review the results  
6. Generate a report  

---

## 3. Getting Started

Before running a check, make sure:

- The design file (`.def`, `.lef`, or `.gds`) is available  
- The file is readable  
- The required ruleset is selected  

---

## 4. Running a Design Check

1. Open VTran.  
2. Select **Design Check**.  
3. Specify the design file location.  
4. Choose a ruleset (`standard`, `strict`, or `custom`).  
5. Set the minimum severity level.  
6. Click **Run Check**.  

VTran submits the job and displays the status (`queued`, `running`, `completed`, or `failed`).

---

## 5. Reviewing Results

When the check completes, open the results page to view:

- Total number of findings  
- Breakdown by severity (error, warning, info)  
- Rule ID, location, and description of each finding  

---

## 6. Generating a Report

1. Open the completed check.  
2. Select **Generate Report**.  
3. Choose the format (PDF or CSV).  
4. Specify the output location.  
5. Click **Generate**.  

---

## 7. Troubleshooting

| Problem                        | Possible Cause                     | Solution                                      |
|--------------------------------|------------------------------------|-----------------------------------------------|
| Check fails to start           | Design file cannot be accessed     | Verify the file path and permissions          |
| Check fails during processing  | Invalid or unsupported design data  | Review the log and correct the input          |
| Expected findings are missing  | Minimum severity is set too high   | Lower the severity setting and re-run the check |

---

## 8. Related Documentation

- VTran Installation Guide  
- VTran Configuration Guide  
- VTran API Reference  
- VTran Release Notes  

---

**End of Document**
