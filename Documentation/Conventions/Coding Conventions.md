# Coding Conventions

Conventions are important, especially when working together in a team, to keep
the code base maintainable over time. Following the conventions is not additional
work (unless possibly slightly in the beginning), but saves a lot of work.

## 1. Naming, formatting etc.

By default, the standard C# conventions by Microsoft apply:
* [Microsoft naming guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines)
* [Microsoft C# coding conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)

In cases that are not covered by the official coding conventions, a community(*1) consensus
should be researched, e. g. highly rated answers on Stack Overflow or Software Engineering
Stack Exchange, or similar.

(*1) *Specifically the professional C# community. Be vary of advice from the Unity
forums and similar sources that are frequently used by hobbyists, where seemingly
a consensus might be reached simply due to the ubiquity of ill-advised practices.*

**Note:**
Unity itself is not very consistent with their conventions (e. g. in sample projects
and code examples), so "official" code examples from Unity, and code from the Unity
community, are not necessarily a good example of good practices and conventions.

## 2. Unity-specific coding conventions

Some things occur disproportionally often in Unity development compared to C# in general,
and are worth their own convention.

### 2.1 SerializeField attributes (and other attributes)

Attributes (e. g. `[Serializable]`) in general are on the line above. The exception
is the `[SerializeField]` attribute, which should be placed on the same line, since
it is more readable especially with longer lists of serialized fields, and allows
for using blank lines to group related serialized fields together, which is not
possible in the second example below.

**Do this ...**
```c#
[SerializeField] private Canvas _mainUiCanvas;
[SerializeField] private TMP_Text _playerNameLabel;
[SerializeField] private TMP_InputField _playerNameInputField;
[SerializeField] private Button _confirmButton;

[SerializeField] private string _playerId;
[SerializeField] private string _playerName;
```

**... instead of this:**
```c#
[SerializeField]
private TMP_InputField _playerNameInputField;

[SerializeField]
private Button _confirmButton;

[SerializeField]
private Canvas _mainUiCanvas;

[SerializeField]
private TMP_Text _playerNameLabel;

[SerializeField]
private string _playerId;

[SerializeField]
private string _playerName;
```

## 3. Comments

### 3.1 Documentation comments

**Do** write documentation comments, especially on classes and public members
(if beneficial).

Example:

```c#
/// <summary>
/// A dialog which handles the lifetime of a view.
/// </summary>
public abstract class AbstractDialog<T> where T : AbstractView
```

### 3.2 Inline comments

**Avoid** inline comments (unless absolutely necessary). When considering to add
a comment to explain a piece of code, first try to improve the code.

**But:** **Do** add inline comments when necessary.

**Do this ...**
```c#
var playerHealth = ...
```

**... instead of this:**
```c#
// The player's health.
var hp = ...
```

To explain *why* a piece of code exists, consider whether it is absolutely necessary for
the next developer to know (immediately). If not, consider putting that information into
the commit message instead, so that a future developer (including yourself) can find the
information on demand, but is not confronted with it when maintaining the code.

### 3.3 TODO comments

The code base should contain the current, valid state of the code. The Git history is
for documenting the past, and the GitHub project management tools are for planning the
future.

- Use TODO comments only locally as a reminder of what you need to before you commit.
- Do not commit TODO comments.
- If it must to be done, do it now.
- If it can/should be done later, create a GitHub issue or ticket instead.

### 3.4 Commented code

Commented-out code often stays in the codebase forever, because future developers do not
know whether it should be uncommented or not. In the worst case, it confuses developers,
even if it has been outdated for a long time.

The code base should contain the current, valid state of the code.

- Do not comment out code (except temporarily for debugging).
- Before you commit, decide whether to uncomment or delete the commented-out code. If it
is ever needed again, we can still find it in the Git history.
- If you find code that is already commented out, decide whether it seems to be commented
out by mistake and should be uncommented. When in doubt, delete it.
