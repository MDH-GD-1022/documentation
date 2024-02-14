AchievementSystem
===
Achievement System instances manage [Stats](Stats.md) and [Achievements](Achievements.md).
Once an achievement of the system is achieved, the `OnAchieved` event will be invoked.
If an achievement makes progress, the `OnProgressMade` event will be invoked.

---
# Stats
Full article: [Click here](Stats.md)

Stats have to be created using the `AddStat` function of an AchievementSystem instance.
Stats can contain any value of a specified type.
Their value can be changed using their `Value` property.
Once the value is changed, stats will invoke their `OnValueChanged` event.

---
# Conditions
Full article: [Click here](Conditions.md)

Conditions are objects that can check something. They keep track of their current state. It can be accessed using using the `IsTrue` property.
Whenever their state changes, conditions will invoke their `OnConditionTrue` or `OnConditionFalse` events.
Conditions can be updated by calling their `Update` function. This will check the condition and update the state.

---
# Achievements
Full article: [Click here](Achievements.md)

Achievements are defined as a set of conditions. Once all conditions are true simultaneously, the achievement is achieved.
Achievements have to be created using the `AddAchievement` function of an AchievementSystem instance.
To check if progress was made you can use the `TryUpdateAchievement` function
Once progress is made towards completing an achievement, the Achievement System will invoke the `OnProgressMade` event.
Once an achievement is achieved, the Achievement System will invoke the `OnAchieved` event.
