# Mattermost Google Calendar Plugin (ALPHA)

A google calendar plugin for Mattermost client which allows you to create, delete, and get notifications from your google calendar events.

## Features

- Create events
- Delete Events
- Get 10 minute notifications
- Get event updates
- Status is set to Do Not Disturb when in a event (Manually required to reset it)
- Get invitations request within Mattermost and reply to them instantly
- Get upcoming calendar events
- Get a summary for any day you like

## Installing

Clone this repo and do a `make`. You will need to upload this to your mattermost instance through the system console and provide it a Client secret and Client ID.
These can be obtained through the following procedure:

1. Go to [Google Cloud Dashboard](https://console.cloud.google.com/home/dashboard) and create a new project.
2. After creating a project click on `Go to APIs overview` card from the dashboard which will take you to the API dashboard.
3. Make sure Google Calendar API is enabled. 
    1. Click on Library from the left menu or go to [API library](https://console.cloud.google.com/apis/library)
    2. Search for "Google Calendar API" and click the card
    3. Click the ENABLE button
4. Configure the `OAuth Consent Screen`
    1. click `Configure consent screen` from the left menu
    2. choose User Type (internal or external)
    3. Application Name: mattermost-plugin-google-calendar
    4. Enter value of `Authorized domains` `<Mattermost server URL>`
5. Select `Credentials` from the left menu or use this link [API and Services](https://console.cloud.google.com/apis/dashboard)
    1. Now click on `Create Credentials` dropdown and select `Oauth client ID` option.
    2. Select Application type: `Web Application`
    3. Name: `Mattermost Google Calendar Client`
    4. `Authorized Javascript Origins:` - `<Mattermost server URL>` 
    5. `Authorized redirect URIs:` - `<Mattermost server URL>/plugins/com.mattermost.google-calendar/oauth/complete`
6. After creating the Oauth client, copy the Client ID and secret.
7. Upload the plugin to Mattermost and go to `Google Calendar Plugin settings`. Paste the client id and secret and select a user for the plugin to post event messages with.
8. Enable the plugin and you should be able to see event reminder notifications.

## Installing For Development
You will be required to follow the above steps to acquire a Client ID and Client secret.

**Note: Google will need you to verify the domain**
1. You can use Python SimpleHTTPWebServer to set one up
2. `python3 -m http.server 8065`
3. open `localhost:8065` and upload the file google provides to verify the domain.
4. Afterwards, you can close SimpleHTTPWebServer and run your Mattermost Server

**Setup Mattermost**
1. Clone the repo and make sure `mattermost server` and `mattermost webapp` is up and running.
2. Use `ngrok` or any other tunnel provider to expose the mattermost server port (8065) to Internet. The command to create a tunnel is `ngrok http 8065`
3. `make deploy` to deploy the plugin

## Contributing

If you are interested in contributing, please fork this repo and create a pull request!

## To-Do's / Future Improvements

- Change response to event within mattermost
- Show conflicts when invited to event with other events on your calendar
- Better error logging / handling
- Optimizations in cron jobs for reminding users about 10 minutes until event as well as user in event
- Code refactoring
- More commenting throughout code to explain what's going on
- Set the calendar user wants to sync with (Currently it uses primary calendar)
- Customize reminder time (user can set if they want anything other than 10 minutes)
- Include a web app portion which displays the events for a particular day without user needing to enter commands

## Authors

* **Hossein Ahmadian-Yazdi** - [Hossein's Github](https://github.com/hahmadia)

## Acknowledgments

* Thanks to [Waseem18 Notification Plugin](https://github.com/waseem18/mattermost-plugin-google-calendar) for the code inspiration
* Thanks to [Mattermost Github Plugin](https://github.com/mattermost/mattermost-plugin-github) for code structure
* Created as a submission for Mattermost Hackathon 2019!!
