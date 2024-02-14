Conditions
===
Conditions are objects that can check something. They keep track of their current state. The state can be accessed using using the `IsTrue` property.
Whenever their state changes, conditions will invoke their `OnConditionTrue` or `OnConditionFalse` events.
Conditions can be updated by calling their `Update` function. This will check the condition and update the state.

---
# Stat Conditions
It is recommended to mostly use stat based conditions for achievements as these update automatically, whenever stats change.
There are multiple different predefined types of stat based conditions

- **StatGreaterCondition**s are true when a specific stat's value is greater than a specified value.
- **StatGreaterEqualsCondition**s are true when a specific stat's value is greater than or equal to a specified value.
- **StatEqualsCondition**s are true when a specific stat's value is equal to a specified value.
- **StatLesserEqualsCondition**s are true when a specific stat's value is lesser than or equal to a specified value.
- **StatLesserCondition**s are true when a specific stat's value is lesser than a specified value.
- **StatTrueCondition**s are true when a specific bool stat's value is true.
- **StatFalseCondition**s are true when a specific bool stat's value is false.

---
# Custom Conditions
You can create your own condition types.
The following is an example condition that checks if a uint stat holds the value 0.
As it's a StatCondition, it will automatically update whenever the Stat's value changes.
```cs
public class StatZeroCondition : StatCondition<uint>
{
    public StatZeroCondition(Stat<uint> stat)
        : base(stat) { }

    protected override bool IsConditionTrue()
    {
        return Stat.Value == 0;
    }
}
```

The AchievementBuilder allows using any Condition for its achievements using the `AddCondition` function.
This allows you to create extension methods for any condition types you want.
```cs
public static class AchievementBuilderExtension
{
    public static AchievementBuilder AddStatZeroCondition(this AchievementBuilder achievementBuilder, Stat<uint> stat)
    {
        return achievementBuilder.AddCondition(new StatZeroCondition(stat));
    }
}
```
