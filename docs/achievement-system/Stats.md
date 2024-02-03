Stats
===
The achievement system heavily relies on keeping track of stats.
Stats can be any value of any type stored under any ID you choose to provide.
You can change the value of stats, which will call the OnValueChanged Event on the stat object.

### Adding Stats
Considering you already have an achievement system that uses strings as ids for both stats and achievements:
```cs
AchievementSystem<string, string> achievementSystem = new();
```

Adding a stat is as easy as:
```cs
achievementSystem.TryAddStat<uint>("Tea spilled", 0);
```
This stat is of type `uint` and is supposed to track the amount of times that tea was spilled.
The second parameter specifies the initial value of the stat. In this case it's 0. No tea has been spilled yet.

### Updating Stats
Using the same AchievementSystem instance as before, you can access the "Tea spilled" stat object using the `TryGetStat` method.
You can then use the `Value`` property of a stat object to get or set the value to anything you want.
```cs
public void SpillTea()
{
    if (achievementSystem.TryGetStat<uint>("Tea spilled", out Stat<uint> stat))
    {
        stat.Value++;
    }
}
```

### When to update?
If you use this a lot of times, it may be more suitable to cache the reference to the stat object.
```cs
public class TeaSpiller
{
    private readonly Stat<uint> _teaSpillStat;

    public TeaSpiller(Stat<uint> teaSpillStat)
    {
        _teaSpillStat = teaSpillStat;
    }

    public void SpillTea()
    {
        _teaSpillStat.Value++;
    }
}
```

### What if the stat doesn't exist yet?
If the stat you want to update doesn't yet exist, you can use the `TeySetStat` method.
```cs
public void SpillTea()
{
    achievementSystem.TrySetStat<uint>("Tea spilled", 10)
}
```
