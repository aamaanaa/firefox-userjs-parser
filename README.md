# firefox-userjs-parser
Parser / validator / updater for firefox user.js files

> [!IMPORTANT]
> this will be released when i am done making it!

**finished so far**:
- [x] parsing of user.js file

**@TODO**:
- [ ] a lot of stuff

## Why is this needed?

> NOTE: this repo = arkenfox, betterfox and so on

basically, i have my own user.js with some other tweaks not in this repo. so the problem i now have is that i do not have a easy way to check for new updates in this repo and compare to my own user.js, and also doing proper validation on the file.

by making this i can find out new, removed, modified prefs and check the formatting of the user.js file, whilst also keeping my own added prefs intact.

since i have quite a lot of stuff from this repo but a lot of changes in them simply pulling and downloading a prefs file from this repo and replacing my own user.js will not work at that will f up my entire setup.

it should also i think handle backups of old user.js file and so on and on

this is just a rough idea to implement this. i suppose ill need to think how i am planning to do this. then i will implement test it and prob put it on a new repo (maybe). my 700 lines of user.js become quite hard now lol. i wll maybe think of other idea's. idk.

i do have to note that this will be some kind of a personal tool but maybe it will be usefull to others idk ?

##  How it works
the user.js file is parsed with these rules in mind:

- all extra spaces removed if there are any.
- all comments behind the user pref saved
- all boolean, string, or int style prefs parsed (dev note: ```map[string]any``` + parser func()
- indentifies duplicates
- sorts the prefs based on their first key, eg `browser.cache.disk.enable` > `browser` and groups them together in a ordered map. this will make our user.js more structured per category
  - then optionally do this for every single . so sort by `browser.cache` and so on.
- and more to come...

the final result looks something like so

```json
"browser.link.open_newwindow.restriction": {
    "Value": false,
    "Comment": "disallow pop ups with newwindow event"
},
```

Now, this is *clear, sexy, and well structured*! So, easy to share and give! and more important: easy to use for the rest of the upcomming functionality!

we can do stuff with this like comparing to other user.js from online resources, save it, back up it, share it online. whatever.

### parsing other user.js files
The plan is to do the same for other user.js file fro example arken fox. The we do the same for them, by downloading and storing / parsing them in memory.

We could then compare the output of out own with these questions:

- what is updated? 
- what is removed?
- what is added?

This would make it extremly clear if there are updates in the external userjs repo, and would be able to for example automaticly update our user.js should the user choose to do this.
