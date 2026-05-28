# Create-room-mailbox.md

3 Objective

Create a room mailbox for meeting scheduling.

Steps

1. Open Exchange Admin Center

2. Navigate to Recipients > Resources

3. Create Room Mailbox

4. Configure room capacity

5. Enable Auto Accept

6. Configure conflict prevention



# PowerShell Configuration

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```
