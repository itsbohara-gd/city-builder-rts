# Clean Code

There are whole books about the topic of Clean Code, and a lot of information
can be found online. Here is a summary of some of the most important points.

## 1. Formatting and conventions

Format the code according to convention (including white space and braces).
Follow the established naming conventions for `ClassNames`, `MethodNames`,
`_fieldNames` etc.

## 2. Choose clear names

Take your time when choosing a name. A few minutes of thinking can save someone hours
of debugging because of a misunderstood method name later on.

A common saying goes that naming things is a very difficult part of programming. But the
difficult part is choosing *what* to name. The name itself should be obvious, and if it
is not, reconsider the thing, not the name. Choose the right metaphors, and invest in
basic writing skills.

### In general

- Avoid abbreviations, e. g. `message`, not `msg`. Exception: Well established abbreviations,
e. g. `args` for `arguments`, and abbreviations that are proper names or acronyms,
e. g. `id`, `HTML` or `NPC` (in the case of something like `NPC`, the context is important;
when in doubt, use the full name, e. g. `NonPlayerCharacter`).
- Make names as short as possible, but as long as necessary. If e. g. a method name,
when as long as necessary, would become very long, consider splitting the method
into 2 methods. Add a documentation comment for important information that does not
necessarily need to be part of the name.
- Do your best to spell correctly. When in doubt, look up the word.
- Use English only. This applies to everything related to code (i. e. names, comments etc.).
Don't be tempted to use e. g. German words just because the problem domain is in German. Non-german
speakers need a good translation anyway, so find a good English translation and document the domain
name in the original language as a docstring.

### Class names

- A class name should describe/identify a concept. Name it *directly* after the concept.
If it is not obvious how the class should be named, reconsider the whole class. Note: It
does not need to be a thing, it can be an abstract concept. It can also be a made-up concept.
But it should be some concept.
- Avoid suffixes like `SomethingManager`, since they do not mean anything. If you want
to name a class e. g. `SoldierManager`, consider `Army`.

### Method names

- A method name should be a verb (or verb phrase) in the imperative form.
- It can be a simple verb (e. g. `Close`) or a verb and noun (e. g. `SpawnEnemies`).
- Also consider the parameters for readability, e. g. `GetPlayerBy(PlayerId id)` instead of
`GetPlayerById(PlayerId id)`.
- Aim for shorter and more general names for public methods, and longer and more
specific names for private methods. E. g. `public void SpawnEnemies`, but
`private void SpawnWhiteFiguresForFirstRound`.

### Variable names

- Use local variables to describe intermediate results and hard to read expressions, e. g.:

Do this ... :
```c#
var blockedDamage = damage - (player.Armor / damage);
var appliedDamage = damage - blockedDamage;
var remainingHealth = player.Health - appliedDamage;
player.Health = remainingHealth;
```
... instead of this:
```c#
player.Health = player.Health - (damage - (damage - player.Armor / damage));
```

## 3. Readable code

Besides the naming of things in the code, write the code in a way that the next
developer can simply read it top-to-bottom and understand it immediately.

Consider the metaphor of a cooking recipe (i. e. a simple list of ingredients followed
by a list of instructions) and the metaphor of a written story (i. e. simply reading
from top to bottom, left to right, and being able to visualize what's happening).

**Examples:**

```c#
// This example is similar to the cooking recipe metaphor:
// First you list your "ingredients", i. e. the things you will work with,
// then you apply some simple steps on them.
private void SaveGameState()
{
    var player1 = GetPlayer(playerIndex: 0);
    var player2 = GetPlayer(playerIndex: 1);
    var player1Figures = GetFigures(playerIndex: 0);
    var player2Figures = GetFigures(playerIndex: 1);

    var gameStateSnapshot = new GameState(
        player1,
        player2,
        player1Figures,
        player2Figures
    );
    _saveGameService.Save(gameStateSnapshot);
}
```
_________________________

```c#
// This example is similar to the cooking recipe metaphor (although
// without ingredients in this case). All individual steps are on
// the same abstraction level.
private void InitializeGame()
{
    InitializePlayers();
    CreateBoard();
    SpawnFigures();
}
```
_________________________

```c#
// This example is closer to the written story metaphor:
// Although the calculations may not be obvious, each line represents an
// intermediate result, and by reading from top to bottom (even just the
// left side of each assignment) you can follow what's happening.
private void ApplyDamage(Player player, float damage)
{
    var blockedDamage = damage - (player.Armor / damage);
    var appliedDamage = damage - blockedDamage;
    var remainingHealth = player.Health - appliedDamage;
    player.Health = remainingHealth;
}
```
