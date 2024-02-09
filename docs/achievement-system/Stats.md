Stats
===
The achievement system heavily relies on keeping track of stats.
Stats can be any value of any type stored under any ID you choose to provide.
You can change the value of stats, which will call the `OnValueChanged` Event on the stat object.
---
## Adding Stats
Considering you already have an achievement system that uses strings as ids for both stats and achievements:
```cs
AchievementSystem<string, string> achievementSystem = new();
```

Adding a stat is as simple as:
```cs
achievementSystem.TryAddStat<uint>("Frogs kissed", 0);
```
This stat is of type `uint` and is supposed to track the amount of times that frogs were kissed.
The second parameter specifies the initial value of the stat. In this case it's 0. No frogs have been kissed yet.

### Overloads
There is an optional out parameter that allows retrieving the newly created stat instantly.
```cs
achievementSystem.TryAddStat<uint>("Chameleons found", out Stat<uint> stat, 0);
```

Providing no initial value, will make the stat use the Type's default value.
```cs
achievementSystem.TryAddStat<uint>("Parrots greeted");
achievementSystem.TryAddStat<uint>("Porcupines hugged", out Stat<uint> stat);
```
---

## Retrieving Stats
Using the same AchievementSystem instance as before, you can access any stat object using the `TryGetStat` method.
```cs
achievementSystem.TryGetStat<uint>("Frogs kissed", out Stat<uint> frogsKissed);
```
---

## Updating Stats
Once you have access to a stat object, you can modify its `Value` property.
The achievement system will update all conditions and achievements in the background.
```cs
public void KissPhyllobatesTerribilis()
{
    frogsKissed.Value++;
}
```

If you don't have access to a stat object and are uncertain whether the stat you want to update even exist, you can use the `TrySetStat` method.
```cs
achievementSystem.TrySetStat<uint>("lemons slayed", 10)
```
