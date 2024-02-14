Stats
===
Stats can contain any value of a specified type.
Stats have to be created using the `AddStat` function of an AchievementSystem instance.
Their value can be changed using their `Value` property.
Once the value is changed, stats will invoke their `OnValueChanged` event.

---
# Adding Stats
Stats can only be created using an Achievement System instance.

In the following, an Achievement System that uses string ids will be used.
```cs
AchievementSystem<string, string> achievementSystem = new();
```

The most simple way to add a stat of a type is to only provide a stat ID.
The Achievement System will then create a new Stat of the specified type and store it under the provided id.
The initial value will be the Type's specified default. (in this case: 0)
```cs
achievementSystem.AddStat<uint>("frogs kissed");
```

## Optional Parameters
It is possible to provide a value, which will then be used as the stat's initial value instead of the Type's specified default.
```cs
achievementSystem.AddStat<uint>("chameleons found", 5);
```

It is possible to instantly get a reference to the created stat by providing an out parameter.
```cs
achievementSystem.AddStat<uint>("porcupines hugged", out Stat<uint> stat);
```

## Exceptionless Try Methods
`AddStat` will throw an exception, if the Achievement System already contains a Stat using the same type and id.

Use `TryAddStat`, if you don't want the code to throw exceptions. This function will return a bool indicating whether or not the operation was successful.
```cs
achievementSystem.TryAddStat<uint>("frogs kissed");
achievementSystem.TryAddStat<uint>("chameleons found", 5);
achievementSystem.TryAddStat<uint>("porcupines hugged", out Stat<uint> stat);
```

---
# Retrieving Stats
Once you have created a stat in the Achievement System, you can get access to the stat object by using `GetStat`.
Access to the Stat object allows modifying it's value.

```cs
achievementSystem.GetStat<uint>("frogs kissed").Value++;
```

## Exceptionless Try Method
`GetStat` will throw an exception, if the Achievement System can not find the stat.

Use `TryGetStat`, if you don't want the code to throw exceptions. This function will return a bool indicating whether or not the operation was successful. The stat will be provided using an out parameter.
```cs
if (achievementSystem.TryGetStat<uint>("chameleons found", out Stat<uint> stat))
    stat.Value++;
```

---
# Changing a Stat's value
If you only want to modify a Stat's value and don't need the Stat Object, you can use `SetStat` instead.

```cs
achievementSystem.SetStat<uint>("porcupines hugged", 10);
```

## Exceptionless Try Method
`SetStat` will throw an exception, if the Achievement System can not find the stat.

Use `TrySetStat`, if you don't want the code to throw exceptions. This function will return a bool indicating whether or not the operation was successful.
```cs
achievementSystem.TrySetStat<uint>("Elephants hidden", 15);
```
