# tgbot❤
![Typing SVG](https://readme-typing-svg.herokuapp.com/?lines=🅆🄴🄻🄲🄾🄼🄴+🅃🄾+🅂🄰🄽🅃🄷🄾🅂🄷+🄶🅁🄾🅄🄿+🄼🄰🄽🄰🄶🄴🄼🄴🄽🅃+🄱🄾🅃!;A+simple+Group+modular+bot!;and+all+futures!)
</p>
<center><a href="https://t.me/santhu_music_bot">
    <img src="http://ForTheBadge.com/images/badges/made-with-python.svg">
  </a></center><br>
<br>

Originally a simple group management bot with multiple admin features, it has evolved, becoming extremely modular and 
simple to use.

Can be found on telegram as [കൊച്ചുമുതലാളി](https://t.me/kochubot).

Kochu and I are moderating a [support group](https://t.me/Keralabots), where you can ask for help setting up your
bot, discover/request new features, report bugs, and stay in the loop whenever a new update is available. Of course
I'll also help when a database schema changes, and some table column needs to be modified/added. Note to maintainers that all schema changes will be found in the commit messages, and its their responsibility to read any new commits.

Join the [news channel](https://t.me/Mo_Tech_YT) if you just want to stay in the loop about new features or
announcements.

Alternatively, [find me on telegram](https://t.me/jithumon)! (Keep all support questions in the support chat, where more people can help you.)


[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/Podilisanthosh/Rose-Bot.git)<br>
There is also a [tutorial video](https://youtu.be/wKL90i3cjPw) if you want any help on creating heroku clone.
[![telegram badge](https://img.shields.io/badge/Support-Group-30302f?style=flat&logo=telegram)](https://telegram.dog/keralabots)
[![telegram badge](https://img.shields.io/badge/Update-Channel-30302f?style=flat&logo=telegram)](https://telegram.dog/kochuUpdates)



## Starting the bot.

Once you've setup your database and your configuration (see below) is complete, simply run:

`python3 -m tg_bot`


## Setting up the bot (Read this before trying to use!):
Please make sure to use python3.6, as I cannot guarantee everything will work as expected on older python versions!
This is because markdown parsing is done by iterating through a dict, which are ordered by default in 3.6.

### Configuration

There are two possible ways of configuring your bot: a config.py file, or ENV variables.

The prefered version is to use a `config.py` file, as it makes it easier to see all your settings grouped together.
This file should be placed in your `tg_bot` folder, alongside the `__main__.py` file . 
This is where your bot token will be loaded from, as well as your database URI (if you're using a database), and most of 
your other settings.

It is recommended to import sample_config and extend the Config class, as this will ensure your config contains all 
defaults set in the sample_config, hence making it easier to upgrade.

An example `config.py` file could be:
```
from tg_bot.sample_config import Config


class Development(Config):
    OWNER_ID = 254318997  # my telegram ID
    OWNER_USERNAME = "SonOfLars"  # my telegram username
    API_KEY = "your bot api key"  # my api key, as provided by the botfather
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # sample db credentials
    MESSAGE_DUMP = '-1234567890' # some group chat that your bot is a member of
    USE_MESSAGE_DUMP = True
    SUDO_USERS = [18673980, 83489514]  # List of id's for users which have sudo access to the bot.
    LOAD = []
    NO_LOAD = ['translation']
```

If you can't have a config.py file (EG on heroku), it is also possible to use environment variables.
The following env variables are supported:
 - `ENV`: Setting this to ANYTHING will enable env variables

 - `TOKEN`: Your bot token, as a string.
 - `OWNER_ID`: An integer of consisting of your owner ID
 - `OWNER_USERNAME`: Your username

 - `DATABASE_URL`: Your database URL
 - `MESSAGE_DUMP`: optional: a chat where your replied saved messages are stored, to stop people deleting their old 
 - `LOAD`: Space separated list of modules you would like to load
 - `NO_LOAD`: Space separated list of modules you would like NOT to load
 - `WEBHOOK`: Setting this to ANYTHING will enable webhooks when in env mode
 messages
 - `URL`: The URL your webhook should connect to (only needed for webhook mode)
 - `BMERNU_SCUT_SRELFTI`: No. of custom filters which can be set in each group

 - `SUDO_USERS`: A space separated list of user_ids which should be considered sudo users
 - `SUPPORT_USERS`: A space separated list of user_ids which should be considered support users (can gban/ungban,
 nothing else)
 - `WHITELIST_USERS`: A space separated list of user_ids which should be considered whitelisted - they can't be banned.
 - `DONATION_LINK`: Optional: link where you would like to receive donations.
 - `CERT_PATH`: Path to your webhook certificate
 - `PORT`: Port to use for your webhooks
 - `DEL_CMDS`: Whether to delete commands from users which don't have rights to use that command
 - `STRICT_GBAN`: Enforce gbans across new groups as well as old groups. When a gbanned user talks, he will be banned.
 - `WORKERS`: Number of threads to use. 8 is the recommended (and default) amount, but your experience may vary.
 __Note__ that going crazy with more threads wont necessarily speed up your bot, given the large amount of sql data 
 accesses, and the way python asynchronous calls work.
 - `BAN_STICKER`: Which sticker to use when banning people.
 - `ALLOW_EXCL`: Whether to allow using exclamation marks ! for commands as well as /.

### Python dependencies

Install the necessary python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all necessary python packages.

### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I use postgres, so I recommend using it for optimal compatibility.

In the case of postgres, this is how you would set up a the database on a debian/ubuntu system. Other distributions may vary.

- install postgresql:

`sudo apt-get update && sudo apt-get install postgresql`

- change to the postgres user:

`sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

`createuser -P -s -e YOUR_USER`

This will be followed by you needing to input your password.

- create a new database table:

`createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever db youre using (eg postgres, mysql, sqllite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and db name.

## Modules
### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from tg_bot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.










 
GOKUL JUNIOR COLLEGE 
nd
INTERMEDIATE 2 year {civics} 
important questions 
➢ LONG QUESTIONS {10 MARKS} 
1. Explain the causes for the origin of Indian National Movement? 
2. Explain the salient features of Indian constitution? 
3. Explain the fundamental rights as incorporated in the Indian constitution? 
4. What are the differences between fundamental rights and directive principles 
of state policy? 
5. Describe powers and functions of president of India? 
6. Describe the powers of prime minister of India? 
7. Explain the various factors which led to the agitation for a separate Telangana 
State? 
8. Discuss the formation of Telangana as the New State in the Indian union? 
 
➢ SHORT QUESTIONS {5 MARKS} 
9. Write about the important events during the Gandhian Phase of Indian 
National Movement? 
10. Write about the functions of Supreme Court of India? 
11. Write about election of vice president and his powers and functions? 
12. Write about Powers and Functions of State Governor? 
1 
  
13. Write about Powers and Functions of State Governor? 
14. Explain Powers and Functions of the Chief Minister? 
15. Describe the main Provisions of the 73 Constitution Amendment Act, 1992? 
16. Explain about Central Election Commission? 
17. Elucidate various types of Terrorism in Indian Context? 
18. Explain the Provisions of Gentlemen’s Agreement? 
19. What is E-Governance? 
20. Discuss the merits and demerits of E-Governance? 
21. What is SMART Governance? 
22. Explain any two Features of Indian Foreign Policy? 
23. Briefly describe the Powers and Function of the Secretary General? 
 
➢ VERY SHORT QUESTIONS {2 MARKS} 
24. Moderates? 
25. Preamble? 
26. Universal Adult Franchise? 
27. Socialistic Principles? 
28. Any four Fundamental Duties? 
29. What is an Electoral College, who are the members of Electoral College?  
30. National Emergency? 
31. NITI AYOG? 
32. Balwanth Rai Mehta Committee? 
2 
  
33. L.M Singhvi Committee? {deleted} 
34. Gram Sabha? 
35. Write about Electoral Photo Identity Card {EPIC}? 
36. Coalition Politics at National level? 
37. Forms of Corruption? 
38. Whistle Blowers? 
39. Sakala Janula Samme?  
40. Million March? 
41. In which year the RTI was enacted and enforced? 
42. What is BIMSTEC? 
43. Who are the members of SAARC? 
44. List the main organs of UNO? 
45. Who are the members of BRICS? 
46. What is Panchasheel? 
 
 
 
 
 
 
 
****** 
3 
 
