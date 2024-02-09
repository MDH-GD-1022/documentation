AchievementSystem
===
In order to use the AchievementSystem, you first need to create an instance of the AchievementSystem class. <br/>
This instance serves as the main point of interaction.
it can be used to manage [Stats](Stats.md) and [Achievements](Achievements.md)
```cs
AchievementSystem<string, string> achievementSystem = new();
```

### Stats
Full article: [Click here](Stats.md)

Stats can be any value of any type stored under any ID you choose to provide.

You can add stats using `TryAddStat`, retrieve the stat objects and the current value by calling `TryGetStat`.
Stat objects allow retrieving or changing the value and subscribing to the stat's `OnValueChanged` event.

### Achievements
Full article: [Click here](Achievements.md)

Achievements are defined as a set of conditions.
Once all conditions are true, the achievement is unlocked.

### Custom Stat and Achievement Data
While creating the AchievementSystem instance you can specify two generic types:

- `TStatID` The Type to use as an identifier for stats
- `TAchievementID` The type to use as an identifier for achievements

These can be used for providing any additional data you may need.
