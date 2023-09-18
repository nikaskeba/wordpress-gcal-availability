# WordPress Google Calendar Availability Plugin (Wordpress Calendly Like Tool)

A WordPress plugin that integrates with Google Calendar to display your availability directly on your website. It utilizes a shortcode to embed a calendar view into your WordPress site, allowing visitors to quickly see your availability based on your Google Calendar events.

## Screenshots

<img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screen%20Shot%202023-09-17%20at%201.02.32%20PM.png"><img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screen%20Shot%202023-09-17%20at%201.55.23%20PM.png"><img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screen%20Shot%202023-09-17%20at%201.56.35%20PM.png"><img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screen%20Shot%202023-09-17%20at%201.56.50%20PM.png">

## Features
**Google Calendar Integration**
Integrate Google Calendar to display available and busy slots.
Set up API Key and Calendar ID through the WordPress admin panel.

**Off-Hours Settings**
Configure off-hours for each day of the week through the WordPress admin panel.
Option to add two different off-hours for each day.
Facility to mark a day as "No Availability".

**Booking Form**
Users can book an available slot through a frontend form.
Theform includes fields for name, email, message, date, time slot, and time zone.

**Booking Confirmation**
Sends a booking confirmation email to the admin with the details of the booking.
Sends a calendar invite (.ics file) to the user based on their input email.
Customizable email body for users with booking details.

**Error Handling**
Error handling for invalid time zone input.
Proper feedback on API request failure.

## Live Demo

Hosted on my personal website - <a href="https://skeba.info/book">Link</a>

## Features

- **Calendar Shortcode Integration**: Easily embed a calendar view on any page or post using a shortcode.
- **Google Calendar Integration**: Fetches your availability data directly from your Google Calendar.
- **Customizable Appearance**: Customize the appearance of the calendar to match your website's style.
- **Responsive Design**: Ensures a seamless experience across various devices.
- **Display**: Subtracts your scheduled events from the calendar and displays only the available times.
- **Interval Selection**: User can select 15 min, 30 min, 45 min, or 1 hour time slots.
- 
## Technology Stack

- **JavaScript**: For dynamic and interactive elements.
- **PHP**: Backend development to integrate the plugin with WordPress.
- **Google API**: Utilized to fetch dates and events based on your configured Google Calendar account.

## Installation

### Prerequisites

- A WordPress installation
- Google Account (for Google Calendar access)
- Google Calendar API Key
  
### Step-by-Step Guide

1. Download the plugin ZIP file.
2. Upload the plugin to your WordPress plugins directory.
3. Activate the plugin through the 'Plugins' menu in WordPress.
4. Configure the plugin settings with your Google API credentials and Google Calendar ID.
5. Use the shortcode `[google_calendar_availability]` in your posts or pages to display the calendar.

### Plugin Challenges

#### Finding the best way to display availability
Initially, the plugin was designed to display busy times from the Google Calendar. However, we realized that it would be more user-friendly to display the available time slots instead. To achieve this, we made the following adjustments:

1. **24-hour String for Busy Dates**: We first converted the busy time slots fetched from Google Calendar into a 24-hour string format to facilitate easier processing.

2. **User-Defined Time Blocks**: We introduced a feature that allows users to define their preferred time blocks for availability, providing more flexibility in displaying available slots.

3. **Subtracting Busy Times to Display Availability**: We implemented a functionality where the busy time slots are subtracted from the user-defined time blocks, which then displays only the available time slots to the visitors.

4. **12-hour Format for Availability Display**: To make the display more reader-friendly, the available time slots are then converted to a 12-hour format before being displayed on the website.

**Fetching Off-Hours Settings**

- **Problem**: The `off_hours_settings` variable was not getting the correct data.
- **Solution**: Made sure to fetch the `off_hours_settings` from the WordPress database using the `get_option` function.

**Date and Time Conversion**

- **Problem**: The date was getting converted to December 31, 1969, and the time was not correct in the .ics file.
- **Solution**: Used proper date and time formatting and conversion to match the selected time zone.

**Calendar Invite File Type**

- **Problem**: The .ics file sent had no file type and was not recognized as a calendar file.
- **Solution**: Created a temporary .ics file with the correct headers and content type to ensure it is recognized as a calendar file.

**Email Sending**

- **Problem**: Using headers caused errors and was not feasible to send multiple emails with different subjects.
- **Solution**: Removed the headers and used the `wp_mail` function to send emails without headers, which allowed sending multiple emails with different subjects without any error.

**WordPress Warning**

- **Problem**: Encountered a warning regarding the misuse of the `wpdb::prepare` function.
- **Solution**: Ensured that all values passed to SQL queries are properly sanitized and prepared to prevent SQL injection and remove the warning.
## Contributing

Developed solely by Nicholas Skeba

## License

Free to use but please credit me as the author

## Changelog

###V.1 Beta - Initial launch without caching.

###V.2 Time Fix - Issue 1, Issue 2.

###V.3 Add interval
## Problem / Solutions

### Issue 1: Incorrect Availability Times
Initial Setting of Timezone: The initial step was to correctly set the timezone when fetching the free/busy information from the Google Calendar. This was done using the new DateTimeZone($timezone) function in PHP.

Time Conversion Without Offset: Instead of directly modifying the time with an offset, we first converted the time to the selected timezone without adding an offset. This was to prevent an additional hour being added to the end time.

Accurate Offset Calculation: After converting the time to the selected timezone, we correctly calculated the offset (if necessary) to modify the start and end times accurately. This prevented the one-hour discrepancy that was being observed initially.

### Issue 2: Date String Not Updating
Correct Date String Usage: We ensured that the date string was correctly updated in the jQuery function handling the date change. This allowed the date to update correctly when a new date was selected on the calendar, instead of retaining the initial page load date.

Debugging and Verification: Throughout the process, we logged intermediate values during the conversion and date selection processes. This allowed us to verify that the values were being calculated and updated correctly.

By implementing these solutions, we were able to fix the incorrect availability time calculations and the date string updating issue, thus ensuring that the availability times displayed were accurate and corresponded to the selected date and timezone.

### Issue 3: Fragmented timing
The availability slots were displaying times that were very close to standard half-hour intervals (e.g., 9:31 AM or 11:59 AM), which might not be very convenient for setting appointments and could lead to fragmented schedules.

Solution:
To make the schedule more uniform and appointments more manageable, we have introduced a feature that rounds the availability time slots to the nearest half-hour or hour. This means that times close to 30 minutes past the hour will be rounded to the half-hour mark, and times close to the hour will be rounded to the nearest hour.

For instance:

9:31 AM will be displayed as 9:30 AM
11:59 AM will be displayed as 12:00 PM
Implementation:
We introduced a new function round_time_to_nearest_interval which takes the hour and minute as parameters and returns the rounded hour and minute. This function is called within the display_available_slot function to adjust the start and end times before displaying them.

### Issue 4: ime Interval Selection

### Description
Allow users to select the time interval for appointment slots. Users can choose intervals of 15, 30, 45, or 60 minutes, with the default set to 30 minutes. When the time interval is changed, the available time slots update immediately to reflect the new interval.

***Implementation***
To implement this feature, we added a new dropdown selector to the UI where users can choose their desired time interval. We also updated the `fetchAvailability` function to accept a new parameter, `timeInterval`, which determines the length of the time slots.

Here's a snippet of the new JavaScript code added to handle the time interval change:

```javascript
// Define a variable to hold the selected time interval, defaulting to 30 minutes
let timeInterval = 30;

// Add a change event handler to the time interval selector
$('#time-interval-selector').change(function() {
    timeInterval = parseInt($(this).val());
    console.log("Time interval changed to:", timeInterval, "minutes");

    // Call fetchAvailability here to update the time slots immediately 
    // when the time interval is changed.
    fetchAvailability(selectedDate, selectedTimezone);
});


