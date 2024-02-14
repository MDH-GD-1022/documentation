Achievements
===
Achievements are defined as a set of conditions. Once all conditions are true simultaneously, the achievement is achieved.
Achievements have to be created using the `AddAchievement` function of an AchievementSystem instance.

To check if an achievement was achieved you can use the `IsAchieved` function.
Once an achievement is achieved, the AchievementSystem will invoke its `OnAchieved` event.

To get the current progress of an achievement, you can use the `GetAchievementProgress` function.
To make the system check, if progress was made, you can use the `TryUpdateAchievement` function.
Once progress towards completing an achievement is noticed, the AchievementSystem will invoke its `OnProgressMade` event.

---
# Adding Achievements
To add achievements you need to specify which conditions the achievement should depend on.
This can be done using an AchievementBuilder instance.
```cs
achievementSystem<string, string> achievementSystem = new();
achievementSystem.AddStat<uint>("frogs kissed", out Stat<uint> stat);

achievementSystem.AddAchievement("10 frogs kissed", new AchievementBuilder().AddStatGreaterEqualsCondition(stat, 10));
```

The Achievement Builder uses the fluent pattern for all it's functions.
The creation of a multiconditional achievement may look like this:
```cs
achievementSystem.AddStat<bool>("Hyla arborea kissed", out Stat<bool> hylaArboreaKissed);
achievementSystem.AddStat<bool>("phyllobates terribilis kissed", out Stat<bool> phyllobatesTerribilisKissed);

achievementSystem.AddAchievement
(
    "All frog types kissed",
    new AchievementBuilder()
        .AddStatTrueCondition(phyllobatesTerribilisKissed)
        .AddStatTrueCondition(hylaArboreaKissed)
);
```

It is recommended to mostly rely on stat based conditions. These will update automatically, whenever the stat's value is changed.

You can also create your own types of conditions, if you want to.

---
# Tracking an achievement's progress
If you want to be able to track an achievement's progress, you have to set a progress tracker in the AchievementBuilder.
Progress Trackers are functions that return a float between 0 and 1.

- 0 means that no progress has been made.
- 0.5 means that it's half way done.
- 1 means that it's done.
```cs
achievementSystem<string, string> achievementSystem = new();
achievementSystem.AddStat<uint>("frogs kissed", out Stat<uint> stat);

achievementSystem.AddAchievement(
    "10 frogs kissed",
    new AchievementBuilder()
        .AddStatGreaterEqualsCondition(stat, 10)
        .SetProgressTracker(_ => {return (float)stat.Value / 10;})
);
```

You can use the TryUpdateAchievement function of the achievementSystem to update an Achievement's progress.
```cs
achievementSystem.TryUpdateAchievemend("frogs kissed");
```

This will make the AchievementSystem call the `OnProgressMade` event if necessary
