Achievements
===
Achievements are defined as a set of conditions.
Once all conditions are true, the achievement is unlocked.

## AchievementBuilder
You can use AchievementBuilder instances to specify which types of conditions an achievement should contain.
```cs
AchievementBuilder achievementBuilder = new()
    .AddStatGreaterEqualsCondition("Tea spilled", 10);
```
You can add as many conditions as you like. The AchievementBuilder utilises the fluent pattern.
```cs
AchievementBuilder achievementBuilder2 = new()
    .AddStatGreaterEqualsCondition("Tea spilled", 10);
    .AddStatGreaterEqualsCondition("Frogs scared", 4);
    .AddStatTrueCondition("Is Unlockable");
```

## How to add achievements?
Considering you already have an achievement system that uses strings as ids for both stats and achievements:
```cs
AchievementSystem<string, string> achievementSystem = new();
```

Once you created the achievementBuilder you can pass it as an argument to the achievement system's `TryAddAchievement` function.
This is also the place where you specify which ID to store the achievement under.
```cs
achievementSystem.TryAddAchievement("10TeaSpilled", achievementBuilder);
```

## Stat based Conditions
We recommend using stat based conditions wherever possible.
These solely rely on stats and will update automatically whenever the associated stats change.

- **StatGreaterCondition**s are true when a specific stat's value is greater than a specified value.
- **StatGreaterEqualsCondition**s are true when a specific stat's value is greater than or equal to a specified value.
- **StatEqualsCondition**s are true when a specific stat's value is equal to a specified value.
- **StatLesserEqualsCondition**s are true when a specific stat's value is lesser than or equal to a specified value.
- **StatLesserCondition**s are true when a specific stat's value is lesser than a specified value.
- **StatTrueCondition**s are true when a specific bool stat's value is true.
- **StatFalseCondition**s are true when a specific bool stat's value is false.

## InjectedConditions
Since we don't want to limit you to using our own rudimentary stat tracking system, we also allow conditions which you can pass your own function to.

An **InjectedCondition** is true, when a provided function returns true.

You can use these if you have your own stat tracking system already or if you want more complex conditions without tracking stats.

These can not update automatically however. You will have to call the `TryUpdateAchievement` function in the AchievementSystem to update an achievement that uses injected conditions.


## How to check if achievements are completed?
There are two ways to check if an achievement is achieved:

1. Whenever any achievement completes, the `OnAchievementCompleted` event of the achievement system is invoked. The achievement id is passed as a parameter.
2. Use `IsAchieved` to check if an achievement is achieved.
