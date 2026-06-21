# Troubleshooting Notes

## Overview

This document records troubleshooting performed during the Apache Web Reconnaissance Detection Lab.

---

# Issue 1

## Problem

No results returned for:

```spl
index=main
| stats count by clientip
```

## Cause

The `clientip` field may not have been extracted automatically.

## Resolution

Review available fields or use:

```spl
index=main
| stats count by host
```

Alternatively, create a custom field extraction.

---

# Issue 2

## Problem

No results returned for:

```spl
index=main
status=404
```

## Cause

The dataset may not contain HTTP 404 responses.

## Resolution

Verify status code distribution:

```spl
index=main
| stats count by status
```

---

# Issue 3

## Problem

No results returned for:

```spl
index=main
status=500
```

## Cause

The dataset contains no HTTP 500 Internal Server Error responses.

## Resolution

This is a valid finding and should be documented in investigation notes.

---

# Issue 4

## Problem

No results returned for:

```spl
index=main
"/admin"
```

## Cause

The dataset may not contain requests for administrative pages.

## Resolution

This is a valid investigative outcome and should be documented.

---

# Issue 5

## Problem

No results returned for:

```spl
index=main
("/backup" OR ".bak")
```

## Cause

No backup file requests exist within the dataset.

## Resolution

Document the finding and continue investigation.

---

# General Verification Queries

## Total Events

```spl
index=main
| stats count
```

---

## Available Fields

```spl
index=main
| head 1
```

---

## Source Verification

```spl
index=main
| stats count by source
```

---

## Sourcetype Verification

```spl
index=main
| stats count by sourcetype
```

---

# Lessons Learned

- Missing results do not always indicate a problem.
- Field extraction depends on the sourcetype.
- Always verify available fields before creating detections.
- Threat hunting requires validating assumptions with data.
- Detection logic should be adjusted based on dataset characteristics.
