# Data Directory

This directory contains structured data files used to generate conference content.

## schedule.yaml

The schedule YAML file is the source of truth for the conference schedule. When present, 
the `hooks/schedule.py` MkDocs hook will automatically generate `docs/schedule/index.md` 
during the build process.

Create `schedule.yaml` when the schedule is finalized with the following structure:

```yaml
friday:
  - time: "09:00am - 12:00pm"
    title: "Tutorial Title"
    link: "tutorials.md#tutorial-slug"
    speaker: "Speaker Name"

saturday:
  - time: "08:00 AM"
    title: "Registration Opens & Breakfast"
    speaker: null

sunday:
  - time: "08:00 AM"
    title: "Registration Opens & Breakfast"
    speaker: null
```
