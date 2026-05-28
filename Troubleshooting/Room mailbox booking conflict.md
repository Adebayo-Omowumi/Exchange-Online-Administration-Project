# room-mailbox-booking-conflicts.md

# Problem

Room mailbox accepts overlapping meetings.

# Cause

AllowConflicts setting enabled.

Resolution

Run:

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```

