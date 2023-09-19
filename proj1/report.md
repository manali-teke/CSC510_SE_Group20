# **CSC 510 Software Engineering**

# **Project Report 1**

*Manali Teke, Vaibhavi Shetty, Aditya Sonar, Shivam Ghodke* 

*September 18th, 2023*

**Introduction :**

Our aim in Part I is to run a previously developed project. [Schedule Bot](https://github.com/SEProjGrp5/ScheduleBot) is a discord bot used for managing and scheduling events in Calendar.
 The features of the bot include: scheduling events, deleting events, listing free time and summary of the events, fetching events from Google calendar and calculating travel time to add to a particular schedule.
The discord bot is coded using Python and we use discord to implement the bot.

**Pre-Requisites :**

1. Python
2. Discord Server
3. Discord Bot Developer Account
4. Google Cloud APIs

**Challenges Faced and Steps Followed:**

The project is a simple discord bot developed using Python. However, the were many issues with running the program.
The following are the challenges faced and our approach to solve those challenges:

**1. Python errors in installing required libraries.**

Since the documentation did not mention the exact python version, we faced errors in installing the required libraries. We created a new python environment and installed the libraries by running commands as an administrator.  
*Command used: _pip install requirements.txt --user*

**2. 'TypeError: BotBase.\_\_init\_\_() missing 1 required keyword-only argument: 'intents'' '**

The previous code was missing one argument. So we got the missing argument error. We added the 'intents' argument and the error was resolved.

*Updated code: bot = commands.Bot(command\_prefix='!',intents=discord.Intents.all())*

**3. The Bot couldn't send messages.**

This is one of the difficulties we encountered because the documentation did not clearly specify the bot permissions. We gave all the texting permissions and few permissions to manage the server and then it worked.

**4. Error 403: App not authenticated**

On using the !ConnectGoogle command, we were not redirected to the sign-in page but got a permission denied message. All the steps regarding the installation and signing into google account were followed. We figured out that the error is because the OAuth Consent was not enabled. We enabled the OAuth Consent Screen by entering the application details and adding our email accounts as test users.
The documentation also did not mention that we needed to update some values of the "credentials.json" file. We changed the client\_id, project\_id and the client\_secret values because these values are unique for each google cloud project and user. We were able to successfully connect to Google account which means the !ConnectGoogle command now worked.

*Steps followed :*
1. _Login into Google Cloud Console and select the project._
2. _Go to APIs & Services -\> OAuth Consent Screen._
3. _Enter the project details and add test users._
4. _Change the values for client\_id, project\_id and client\_secrect in credentials.json._

*How to get client\_id, project\_id and client\_secrect in the google cloud console?*
1. _Click on the project drop-down arrow in google cloud console. In the following box that appears there is a list of all the projects associated with that google account and their respective project\_id._
2. _Go to API & Services -\> Credentials -\> Create Credentials -\> OAuth Client ID. Enter the application details. And note the client\_ID and client\_secrect._

**5. Unable to fetch upcoming events from Google calendar.**
The schedule bot has a command called !GoogleEvents that fetches next ten events from the connected google calendar. The google cloud project was set up, the google account was connected and authenticated and yet we could not access the Google Calendar. This was because the google calendar was not able to link with the project. We figured out, since the Google Maps API was used for calculating the time when creating the travel event, we'll need an API for calendars. We enabled the Google Calendar API in the google cloud project console. This worked and the discord bot could successfully fetch the next 10 events from the google calendar.

*Steps followed:*
1. _Open the project in google cloud console._
2. _Go to API & Services -\> API Library. Type Google Calendar API in the search-box._
3. _Click on the API and select Enable API._

**Solutions to avoid similar pain:**

1. Mention the minimum python version.
2. Instead of providing a link to another source on how to create a discord bot, the documentation should've included steps to create a discord server, a discord developer account and what permissions to assign to the discord bot.
3. The documentation just mentioned setting up the project in google cloud and no details on how to link the cloud project into our code. Documentation should've included details about changing project credentials and enabling APIs.
4. The project completely relies on Google Cloud Platform. So we had to sign-up for the Google Cloud credits and it is free only for the first 90 days. They should've used some cheaper or free open-source alternative.

**Drawbacks in previous implementation and plans for Project2:**

1. Since some minor details were missing in the documentation the project couldn't run properly. We shall make sure to include every tiny detail in the future documentation.
2. In the current implementation, we're required to give almost four inputs to schedule one event which is exhaustive. We'll modify the command such that scheduling events will only require single input.
3. In deleteEvent, the bot successfully deletes the event but still shows a message that "Unable to delete event". We'll solve this glitch.
4. We can add a send invites feature when we need to add multiple people to the same event.
