# WordPress Google Calendar Availability Plugin

A WordPress plugin that integrates with Google Calendar to display your availability directly on your website. It utilizes a shortcode to embed a calendar view into your WordPress site, allowing visitors to quickly see your availability based on your Google Calendar events.

## Screenshots

<img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screenshot%202023-09-13%20at%203.21.54%20PM.png"><img style="width:500px;border-style:solid;border-width:2px;border-color:#000;" src="https://github.com/nikaskeba/wordpress-gcal-availability/blob/main/Screenshot%202023-09-13%20at%203.17.29%20PM.png">

## Features

- **Calendar Shortcode Integration**: Easily embed a calendar view on any page or post using a shortcode.
- **Google Calendar Integration**: Fetches your availability data directly from your Google Calendar.
- **Customizable Appearance**: Customize the appearance of the calendar to match your website's style.
- **Responsive Design**: Ensures a seamless experience across various devices.
- **Display**: Subtracts your scheduled events from the calendar and displays only the available times.

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

## Contributing

Developed solely by Nicholas Skeba

## License

Free to use but please credit me as the author

## Changelog

V.1 Beta - Initial launch without caching.
