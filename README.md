# Family Calendar Automation Script

This Google Apps Script automates the creation of a structured weekly schedule in your Google Calendar, helping busy families manage their daily routines and activities.

## Overview

This script creates a week's worth of recurring events in your Google Calendar, including:

- Morning routine (meditation, workout, shower)
- Family meals
- School drop-offs
- Commute and errands
- Day-specific after-school activities
- Evening family time
- Bedtime routines

## Prerequisites

- A Google account
- Access to Google Calendar
- Basic knowledge of Google Apps Script

## Setup Instructions

### Step 1: Get Your Calendar ID

1. Open [Google Calendar](https://calendar.google.com/)
2. Click on the three dots next to your calendar name in the left sidebar
3. Select "Settings and sharing"
4. Scroll down to find your "Calendar ID" (looks like an email address)
5. Copy this ID - you'll need it for the script

### Step 2: Set Up the Script

1. Open [Google Apps Script](https://script.google.com/)
2. Create a new project
3. Delete any default code and paste the entire script
4. Replace `'your_calendar_id'` with your actual Calendar ID (keep the quotes)
5. Save the project (give it a name like "Family Calendar Automation")

### Step 3: Run the Script

1. Select the `createWeekEvents` function from the dropdown menu
2. Click the "Run" button (▶️)
3. If prompted, grant the necessary permissions
4. Check your Google Calendar to see the created events

## Customizing the Script

### Change Event Times

To adjust event times, modify the start and end times in the `createDailyEvents` function:

```javascript
// Example: Change meditation to start at 7:00 AM instead of 6:00 AM
var mindfulnessStart = new Date(date);
mindfulnessStart.setHours(7, 0, 0, 0); // Changed from 6:00 AM to 7:00 AM
var mindfulnessEnd = new Date(date);
mindfulnessEnd.setHours(7, 15, 0, 0); // Changed from 6:15 AM to 7:15 AM
```

### Add New Events

To add a new event, use the pattern shown in the existing code:

```javascript
// Create a new event
var newEventStart = new Date(date);
newEventStart.setHours(21, 30, 0, 0); // 9:30 PM
var newEventEnd = new Date(date);
newEventEnd.setHours(22, 0, 0, 0); // 10:00 PM
calendar.createEvent('Adult Time', newEventStart, newEventEnd, {location: 'Home'});
```

### Change Activity Schedule

The script uses a switch statement to assign different activities to each day of the week. Modify these activities by changing the corresponding case:

```javascript
// Example: Change Tuesday's activity from Art Class to Piano Lessons
case 2: // Tuesday
  calendar.createEvent('Piano Lessons', activityStart, activityEnd, {location: 'Music School'});
  break;
```

### Add Event Details

The script currently sets the event title and location. You can add more details like description or event color:

```javascript
calendar.createEvent(
  'Mindfulness/Meditation',
  mindfulnessStart,
  mindfulnessEnd,
  {
    location: 'Home',
    description: 'Take 15 minutes to center yourself for the day',
    color: CalendarApp.EventColor.PALE_BLUE
  }
);
```

## Advanced Features

### Set Up Recurring Execution

To have this script run automatically every month:

1. Click on the clock icon (Triggers) in the Apps Script editor
2. Click "Add Trigger"
3. Configure:
   - Choose which function to run: `createWeekEvents`
   - Choose which deployment should run: `Head`
   - Select event source: `Time-driven`
   - Select type of time based trigger: `Month timer`
   - Select month of month: `1st`
   - Select time of day: (choose a time like 2:00-3:00am)
4. Click Save

### Handling Holidays and Special Days

The script doesn't currently account for holidays or special days. Consider adding:

```javascript
function isHoliday(date) {
  // Add logic to detect holidays
  return false;
}

// Then in createDailyEvents:
if (isHoliday(date)) {
  // Create holiday-specific events instead
  return;
}
```

## Troubleshooting

### Events Not Appearing

- Check that you used the correct Calendar ID
- Verify you granted the script permission to access your calendar
- Check for any errors in the Apps Script execution log

### Script Execution Errors

- Open the View menu and select "Execution log" to see details about errors
- Common issues include:
  - Invalid calendar ID
  - Time zone issues
  - Exceeding quotas (too many calendar operations)

## Best Practices

1. **Run at Low-Traffic Times**: Schedule the script to run during off-hours
2. **Make Incremental Changes**: Test any modifications on a test calendar first
3. **Clean Up Before Rerunning**: Consider adding a function to delete previous events before creating new ones
4. **Comment Your Code**: Add comments if you make changes to remember your customizations

## Resources

- [Google Apps Script Documentation](https://developers.google.com/apps-script/reference/calendar)
- [Calendar API Quotas](https://developers.google.com/apps-script/guides/services/quotas)
- [Calendar Event Colors](https://developers.google.com/apps-script/reference/calendar/event-color)

## License

This script is provided as-is for personal use.