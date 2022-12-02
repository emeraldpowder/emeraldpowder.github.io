---
layout: page
title: 💾 Player Prefs Snapshots
---

[📥 Get it on Asset Store 📥](https://u3d.as/2Ui2)

### Contents

- [How to use it](#how-to-use-it)
- [Use cases](#use-cases)
- [Configuration](#configuration)
- [Custom fields](#custom-fields)
- [Example scenes](#example-scenes)

**Player Prefs Snapshots** is an editor tool, that allows you to snapshot any number of PlayerPrefs states, and return to any of them at any time

![Menu open window]({{ "/assets/images/prefs-snapshots-menu.png" | relative_url }})

### How to use it

Install the package, and open main window through Tools->Player Prefs Snapshots at the top menu. You can delete sample snapshots that already there, and add your own with "plus" button. Creating snapshot will capture all of your current PlayerPrefs values, and you can return to this state any time by clicking "Load" next to snapshot in this window

![Plugin screenshot]({{ "/assets/images/prefs-snapshots-screen.png" | relative_url }})

Or, if you don't want to open extra windows, you can just open folder with snapshots and load them with context menu:

![Context menu]({{ "/assets/images/prefs-snapshots-context.png" | relative_url }})

*note that you can change folder where snapshots stored in [configuration](#configuration)*

### Use cases

**Easier testing**

It's much easier to test game, when you don't have to manually complete all 100 levels to get to the endgame screen. You can create snapshot at level 99, load it, and get to end of the game in a minute. If you see something not working properly, fix it, load snapshot again, and repeat

**Syncing between computers/team members**

When new team member downloads project, and asks you how to unlock all the game worlds, you don't have to answer "just play for a couple of hours". Now he can just load snapshot "late game progress" that you created, and get a clean and correct state. *Example scene has snapshot "late progress" for this*

**Testing while developing**

Let's say you're developing a tutorial, that should appear only once in a game, at 15th minute of play. Ideally, you should test that it appears on 15th minute, that it doesn't appear on 16th minute, and that it doesn't appear second time. And in case something not working, clear player prefs and test it all again. With this plugin you can snapshot game state at 14th minute, and get to the point of interest in one click. *Example scene has snapshot "just before easter egg" for this*

**Testing game data migrations**

More advanced case, when you are developing big update to your game, and you need specific code to run at first launch after update (maybe to convert old currencies saved from previous version to new, or to remap level completions, to unlock new worlds for old users, etc.). Testing this code is usually a big pain, as you need to switch to old verion in VCS, clear player prefs, play a game to get some progress, then switch to new version, and you have one shot at testing the migration. With this plugin it's much easier - just save several snapshots at old version, and on new version you can load them with one click, and test migration untill you sure it's working perfectly. *Example scene has snapshot "(old) late progress" for this*

### Configuration

You can open `PlayerPrefsSnapshots/Editor/PlayerPrefsSnapshotsConfig.cs` file, to adjust some values there. You can customize path where snapshots is stored, disable window auto refresh if plugin is slowing down Unity, or disable custom fields (columns) in Player Prefs Snapshots window

### Custom fields

*Note that you can always disable custom fields if you don't need them, by setting `CustomFieldsEnabled` to `false`*

Custom Fields are game-specific columns you can add to Player Prefs Snapshots window. Examples of such fields are "completed levels", "coins", or any other parameter you have in your game. To add or edit them, open `PlayerPrefsSnapshots/Editor/PlayerPrefsSnapshotsConfig.cs` class, and find `CustomFields` array. There are 3 sample fields there by deafult. You can delete them, or edit, to fit your game

Every custom field has 3 parameters:
- name, that will show up in the column title
- width, in pixels
- fieldGetter, which is a lambda function that accepts one parameter - current snapshot, and should return this custom field value as a string

For example using this code you can simply display string from PlayerPrefs:
```C#
new PlayerPrefsCustomField("Player name", 100, prefs => prefs.GetString("playerName"))
```

With this code you can format field any way you want:
```C#
new PlayerPrefsCustomField("Tutor", 70, prefs =>
	prefs.GetInt("tutorPassed") == 1 ? "Passed" : "Not passed")
```

Or you can include any complex calculation involving multiple PlayerPrefs keys:
```C#
new PlayerPrefsCustomField("Level", 70, prefs =>
{
    int level = 0;
    for (int i = 0; i < 100; i++)
    {
    	if (prefs.GetInt($"Level{i}Passed") == 1) level++;
    }
    
    return level.ToString(CultureInfo.InvariantCulture);
})
```

Using parameters above, that how Player Prefs Snapshots window might look like:

![Plugin screenshot]({{ "/assets/images/prefs-snapshots-fields-sample.png" | relative_url }})

### Example scenes

In the `PlayerPrefsSnapshots/Example` folder there is a sample scene, containing simple Cookie Clicker clone with it's data saved to PlayerPrefs. Also there are some snapshots from this game scene already created. You can play around in this scene to get an idea of how Player Prefs Snapshots plugin is working

Feel free to delete Example folder and all the snapshots that comes with the asset, when you don't need them

[📥 Get it on Asset Store 📥](https://u3d.as/2Ui2)
