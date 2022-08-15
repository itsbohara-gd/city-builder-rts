# Best Practices

Best practices are (to some extent) subjective, based on experience, and may change
over time. Here are my suggestions for the practices we should follow in this project.

## 1. Follow the conventions

- Coding conventions
- Git conventions
- etc.

## 2. Make it a habit

Make the conventions a habit, so that it becomes easier to follow them than not to
follow them.

> “I'm not a great programmer; I'm just a good programmer with great habits.” - Kent Beck

## 3. Strive for clean code

- Keep it clean while writing it (don't leave the clean-up for later)
- Leave the code cleaner than you found it (the [Boy Scout Rule](https://wiki.c2.com/?BoyScoutRule))
- After you are done, take a few minutes to make it even cleaner (clearer names, fix formatting etc.)

## 4. Test before you commit

- Especially for simple changes, one might easily be optimistic, just change the code and
commit it. Resist that urge. Always run the code before you commit and open a PR. Try
not only the happy case (what should work) but also other cases that players might try.
Make your implementation not only *working*, but *robust*.
- Consider implementing automatic tests (e. g. unit tests) in addition to manual testing.
Even if you decide against adding unit tests: Never break existing unit tests!

## 5. Always review your changes thoroughly before committing ("self review")

- Before every commit, have a careful look at the diff in your Git client. Review each
file and each line to see if the change is intended. Also think of ways to improve the
code/clean it up before committing.
- Never "stage all"!
- Make sure you know what each change means, especially if the changes are not in
code, but e. g. in configuration files or Unity settings and you do not remember
changing them.

## 5. Keep changes narrowly scoped

- To reduce merge conflicts with multiple developers working on the project,
try to keep the changes narrowly scoped.
- Prefer changing prefabs over directly changing scene contents.
- Communicate with your teammates which features you are working on, especially
before working on scenes. Scenes, prefabs and meta files are difficult and
annoying to merge, so merge conflicts are best avoided there.
- When changing code, prefer big changes in few files over many small changes
in many different files, when possible. More abstractly: Try to keep the changes
either vertical or horizontal, but not both.
- Commit often, and open a PR as soon as a meaningful part of a feature is
finished. Merge as soon as possible, so that others can build upon your changes.

## 6. Avoid changing/removing existing public APIs

To reduce conflicts due to multiple developers changing different parts of the
code, keep the following in mind (this applies mainly to **public** members and
classes/interfaces):

- If a new implementation should replace an old one, mark the old one as obsolete.
- Prefer adding e. g. a method overload instead of changing an existing one.

## 7. Avoid prototyping in the development branches

Here we mean prototyping in the sense of "quick and dirty implementation" with the
goal of trying something out and without the intention of keeping it in the long run.

- Use a separate branch, with `prototype` as prefix instead of `feature`.
- Do not merge it into the `develop` or `master`/`main` branches.
- Alternatively, prototype locally, but replace it with your final implementation
before committing.
