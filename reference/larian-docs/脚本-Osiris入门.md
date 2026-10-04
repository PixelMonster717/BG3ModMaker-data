# 脚本-Osiris入门

> 来源：[Scripting:_Introduction_to_Osiris](https://docs.baldursgate3.game/index.php?title=Scripting%3A_Introduction_to_Osiris)
> 抓取自 Larian 官方模组文档

---

Osiris is one of two scripting languages used in Baldur's Gate 3, the other being Anubis. For a complete list of scripting guides, see the Scripting page.

What Is Osiris?
Osiris is an event-driven, declarative language, which means that it listens to various circumstances that occur in the game and produces an event to hook onto when they occur. It's used to modify the world in reaction to events that occur in that world: touching the magical artefact makes the room fill with lava; entering a secret thieves' lair starts a dialogue with their leader; returning an old woman’s lost heirloom completes a quest; leaving an area where a dying man pleads for help kills him.

Osiris is responsible for reacting to game events, getting the information about the current game/object state using queries, and changing the game/object state using calls. (See the Osiris API page for brief descriptions of these terms and for links to existing Osiris events, queries, and calls.)

Operations done with Osiris are meant to be guaranteed because they must happen. If you tell a character to move, it must reach its destination. As such, operations done in Osiris will often have failsafes. For example, if you tell a character to move and the path is blocked by a giant boulder, the character will be teleported instead.

This guide covers the basics of Osiris - goals, events, queries, calls, sections, databases, and rules.

What Is Osiris For?
Osiris’ responsibility is to handle the global world and game states, and the transitions between these states. Osiris has a higher priority over other scripting languages used in the Editor. This means that Osiris calls have a guaranteed execution if the target of the call is valid.
ⓘ Note that the validity of the target is defined by different conditions specific to the call you’re using. For example, you cannot request a character to move using CharacterMoveTo if the character is dead.

Structure
An Osiris program is called a story, and it consists of different goals.

Below is a simple example of an Osiris goal. We’ll go over it in detail.

```
INIT:

DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255);
DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255, “Astarion”);

```
KB:

IF
TextEvent("sayHello")
AND
DB_Characters(_Character)
THEN
DebugText(_Character, "Hello there!");

IF
TextEvent("sayHello")
AND
DB_Characters(_Character, _Name)
AND
Concatenate("Hello there, my name is ", _Name, _ResultString)
THEN
DebugText(_Character, _ResultString);

```
EXIT:

NOT DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255);
NOT DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255, "Astarion");

### Sections

A goal is a text file made up of three sections:

- INIT contains actions that are executed when the goal initialises.

- KB contains rules that become active as soon as the goal finishes initialising.

- EXIT contains actions that are executed when the goal completes.

### Databases

Databases (or DBs) are used to store some data that will be manipulated later.

Every database name should begin with a DB_ and the name itself should be unique for every goal in every mod.

Databases in Osiris are more like a table in an actual database. To store some data, we need to add a row to the desired database. Adding a row is often referred to as defining a fact.

Below is an example of defining a fact for a database:

```
DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255);

We add a new row with a value of the GUIDSTRING type S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255 to a DB called DB_Characters.
It is possible to overload a database, provided it has a different amount of columns:

```
DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255, "Astarion");

Removing a fact from a database is done using the NOT operator:

```
NOT DB_Characters(S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255);

### Rules

Rules consist of one or more trigger conditions, optional extra conditions, and one or more actions. Actions will be executed only when all trigger conditions and optional extra conditions are met.

Below is an example of a rule:

```
IF
TextEvent("sayHello") // Trigger condition
AND
DB_Characters(_Character, _Name) // Trigger condition 2
AND
Concatenate("Hello there, my name is ", _Name, _ResultString) // Extra condition
THEN
DebugText(_Character, _ResultString); // Action

- Osiris reacts to a TextEvent thrown and gets information from DB_Characters.

- Notice that we’re using _Character and _Name as variables to store the output values which DB_Characters returns. It will iterate through every fact in the database and perform a desired action. So, if we had two facts defined in a database, one for Astarion and one for Shadowheart, the rule would be executed twice.

- In this case, we have only one fact in the database, so the value stored in _Character is S_Player_Astarion_c7c13742-bacd-460a-8f65-f864fe41f255 and the value in _Name is Astarion.

- Then Osiris passes the value stored in the _Name variable as a parameter to the Concatenate query.

- When these conditions are met, Osiris calls DebugText to be displayed over the character's head with the concatenated string, which in this case is Hello there, my name is Astarion.

### Execution Order

Osiris execution is completely event-driven, which means that there are no main procedures at which a story starts executing. It can be broken down like this:

Osiris execution order.

- Top-level goals become available as soon as the mod is loaded and a story becomes active.

- When the goal becomes active, its INIT section gets executed.

- The KB section becomes active as soon as the goal starts initialising. Rules, queries, and procedures defined in this goal start getting executed.

- The earliest event that Osiris can react to is GameModeStarted.

- However, rules in the KB section can still react to facts being added to a DB in the INIT section of the same goal, even if the INIT is still being executed.

- GoalCompleted is used for finalising a goal.

- This will execute the EXIT section of the goal and deactivate rules, queries, and procedures defined in this goal.

- Databases defined in the goal will still be active after completing the goal.

- Sub-goals of the goal will become active after this.

- However, the action block (the whole KB section, for example) where GoalCompleted was called will be executed until the end. So, you can add rules below GoalCompleted statement is called, and even reference procedures and queries inside sub-goals, as they become active after GoalCompleted is executed.

All goals are merged into a single story file. Inside this file, all goals are sorted alphabetically. Rules are executed from top to bottom.

So, for example, if you want to use a database defined in another goal, you need to make sure this goal is located before any goal you want to use this database in.

Next Steps
With the basics of Osiris now covered, we recommend heading to Using the Story Editor to learn about the Story Editor, debugging functions, script-specific log files, and how to fix some common build errors.

<div
