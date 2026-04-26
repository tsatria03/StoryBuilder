Intruduction.

Welcome to StoryBuilder!
StoryBuilder is a standalone storytelling engine and mini scripting language designed for creating interactive stories, audio cutscenes, and simple RPG-style experiences.
This app allows writers and developers to build narrative content using plain text scripts that control dialogue, choices, branching paths, and dynamic events.
Stories can react to player decisions, track variables, and change outcomes based on conditions, making each playthrough potentially different.
This scripting system supports interactive menus, branching storylines, randomized events, and reusable story segments, allowing complex narratives to be created without traditional programming.
It also includes systems for managing story states such as variables, collections of data, and player choices so scripts can remember actions and respond to them accordingly.
StoryBuilder can also drive simple gameplay mechanics within stories, including health systems, experience and leveling, inventory tracking, quest progression, and basic combat encounters.
These features allow authors to build lightweight RPG adventures or interactive fiction experiences directly within the scripting environment.
The engine includes integrated audio support for music, ambient sound, sound effects, and cinematic audio sequences, making it especially well suited for accessible audio-focused games and storytelling projects.
Stories can dynamically control sound playback to create immersive environments and dramatic moments.
Additional systems allow stories to generate randomized locations, track journal entries, manage world maps, and save or load progress so longer adventures can be played across multiple sessions.
The language sintaks is designed to remain readable and writer-friendly, while still providing enough power to create complex interactive narratives.
StoryBuilder is intended as a flexible storytelling tool that can be used for interactive fiction, narrative-driven games, audio dramas, or prototype RPG systems, all powered by a lightweight scripting engine.

Command Overview

StoryBuilder provides a large collection of commands used to control narrative flow, dialogue, gameplay systems, audio playback, and player interaction.
Commands are grouped into categories based on their purpose. Each command performs a specific action within the script and can be combined with other commands to create complex interactive stories, mini-games, and gameplay systems.
The following sections describe each command category and explain the purpose of every available command.

Story / Text Commands

These commands control how narrative text is presented to the player. They are responsible for displaying story content, speaking narration, and managing dialog presentation.

text

Displays narrative text using the dialog system. Multiple text lines may be grouped together before being shown to the player.

textsound

Controls whether dialog interface sounds are enabled.
When enabled, dialog interactions such as opening messages, scrolling through text, and copying dialog will play their associated sound effects. When disabled, dialog messages function normally but without sound feedback.
If no argument is provided, dialog sounds are automatically enabled.

say

Speaks a line using the screen reader without opening a dialog window.

title

Changes the application window title. This is commonly used to indicate chapters, scenes, or game modes.

end

Stops execution of the current story script.

Flow Control

Flow control commands determine how execution moves through the script. They allow the story to jump between sections or redirect execution based on events.

label

Defines a location in the script that other commands can jump to.

goto

Moves execution to a specific labeled location in the script.

gotoif

Moves execution to a labeled location only if a condition is satisfied.
For complex conditions, prefer if blocks instead of gotoif.

break

Immediately exits the current loop structure.
When used inside looping commands such as while, for, foreach, or repeat, execution continues with the command that follows the loop block.

continue

Skips the remaining commands in the current loop iteration and begins the next iteration of the loop.

Conditional Logic

Conditional commands allow the script to make decisions based on variables, game state, or player input.

if

Evaluates a condition and executes a command or block of commands if the condition is true.

elseif

Provides an additional condition to check if the previous if or elseif conditions were false.

else

Executes when none of the previous if or elseif conditions were true.
endif

Marks the end of a conditional block. Required when using multi-line conditional logic.

Function System

Functions allow reusable blocks of script logic to be defined and executed from anywhere in the story. This makes large scripts easier to organize and reduces repetition.
Functions may accept arguments and support local variables. Variables created inside a function remain local to that function and do not interfere with other parts of the script.
Functions terminate when a return command or the endfunction command is reached.

function

Defines a reusable block of script commands. Function arguments become local variables available within the function body.

endfunction

Marks the end of a function definition.

call

Executes a previously defined function. Arguments may be passed and will be assigned to the function’s parameters.
When passing a multi-word argument, wrap it in quotes so it is treated as a single value. Without quotes, each word becomes a separate argument.
For example, call greet "Hello, world!" passes one argument, while call greet Hello world passes two separate arguments.

return

Stops execution of the current function and returns control to the point where the function was called.
The return command can also optionally provide a value. When a value is returned, it is stored in the built-in variable lastreturn, which can be referenced elsewhere in the script after the function call.
This allows functions to produce results that can be used by other parts of the story.

Loop Commands

Loop commands allow sections of the script to repeat automatically.
These commands are useful for repeating actions, validating player input, processing lists of values, or running gameplay systems.

while

Repeats a block of commands as long as a condition remains true. The condition is evaluated before each iteration.

endwhile

Marks the end of a while loop block.

for

Repeats a block of commands using a numeric loop variable and defined iteration range.

foreach

Iterates through each element of an array and executes commands for each item.

endfor

Marks the end of a for or foreach loop block.

repeat

Repeats a block of commands a fixed number of times.

Random / Dice Commands

These commands introduce randomness into the story. They can be used for game mechanics, probability systems, or procedural storytelling.

flip

Simulates flipping a coin and randomly produces one of two outcomes.
The result is spoken, displayed to the player, and stored so it can be used later in conditions or game logic.

genpass

Generates a random password using specified character types and length.
The generated password is automatically spoken and stored to be used later.

roll

Simulates rolling dice and stores the resulting values for later use.

spin

Simulates spinning a selection wheel using items stored in an array.
A spinning animation using sound effects is played before the final result is selected and stored. Optional parameters allow customization of spin behavior.

randomchoice

Randomly selects one command from a group of possible commands.

randitem

Selects a random item from an array and stores the result in a variable.

Variable Commands

Variable commands store and manipulate data used throughout the story. Variables may contain text, numbers, or results from player actions.

To reference a variable's value inside text, say, or other output commands, wrap the variable name in angle brackets like <varname>.
When using a variable in a condition such as if, while, or elseif, use the variable name directly without angle brackets.

write

Prompts the player for input and stores the entered value in a variable.

writemode

Configures how the write command handles character input restrictions and cancel behavior.
This command must be called before write to take effect. If not used, write behaves normally with no restrictions applied.

var

Creates a new variable or assigns a value to a variable.

set

Assigns or replaces the value of an existing variable.

add

Adds a numeric value to a variable.

sub

Subtracts a numeric value from a variable.

mul

Multiplies a variable by a value.

div

Divides a variable by a value.

length

Calculates the length of text or arrays and stores the result in a variable.

Menu / Choice Systems

These commands create interactive selections that allow players to choose actions or navigate story branches.

menu

Creates a menu using items stored inside an array.

menumode

Configures how menu and choice commands handle the player pressing escape to cancel.
This command must be called before menu or choice to take effect. The setting persists until changed.
Supported cancel modes are: continue, which is the default and moves on with menuindex set to zero; loop, which re-shows the menu until the player makes a selection; exit, which ends the story; return, which returns from the current function; and goto followed by a label name, which jumps to that label.

menuindex

Stores the numeric position of the selected menu item.

menucom

Executes commands associated with a selected menu item.

question

Displays a multiple-choice question and stores the player’s selected answer.

answer

Executes a command depending on which answer was previously selected.

choice

Creates a structured branching decision block that presents multiple selectable options to the player.

Array System

Arrays are lists of values that can be used for menus, random selection, or structured data storage.

array

Creates a new array and fills it with values.

push

Adds a new value to the end of an array.

pop

Removes the last value from an array.

shuffle

Randomizes the order of values stored in an array.

pick

Selects a random value from an array.

remove

Removes every occurrence of a value from an array.

remove_first

Removes the first occurrence of a value from an array.

remove_last

Removes the last occurrence of a value from an array.

join

Combines all values from an array into a single string.

filter

Creates a new array containing only values that exactly match a specified value. The result is stored in a new array.

sort

Sorts an array alphabetically or numerically.

range

Generates a sequence of numbers and stores them in an array.

Audio / Sound Commands

These commands control sound effects, ambient audio, and music playback during the story.

play

Plays a sound effect.

stop

Stops currently playing sound effects.

amb

Starts looping ambient audio.

ambstop

Stops ambient audio playback.

mus

Starts looping background music.

musstop

Stops background music playback.

silence

Stops all currently playing audio.

cutplay

Plays a cinematic audio sequence and blocks script execution until the sound finishes or is skipped.

Timing / Interaction

These commands control timing and pauses in script execution.

wait

Pauses script execution for a specified amount of time.

waitkey

Pauses execution and displays a prompt telling the player to press Enter. Execution resumes once the player presses the Enter key.

Inventory System

Inventory commands manage items that the player can obtain and carry.

give

Adds an item to the player’s inventory.

recycle

Removes an item from the player's inventory.

inv

Displays the current inventory contents.

invclear

Removes all of the items from the player's inventory.

Quest System

Quest commands manage story objectives and track player progress.

queststart

Creates a new quest and adds it to the quest log.

questcomplete

Marks a quest as completed.

questfail

Marks a quest as failed.

questcheck

Checks whether a specific quest is active or completed and executes a command if it is. This allows scripts to trigger events or dialog based on quest progress without using separate conditional blocks.

quests

Displays the current quest log, listing all active quests by name.

questclear

Removes all quests from the quest system, clearing the quest log entirely.

RPG Mechanics

These commands implement simple role-playing mechanics such as health and experience.

damage

Reduces the player’s health.

heal

Restores the player’s health.

hp

Displays the player's current health status.

xp

Awards experience points to the player.

level

Displays the player's level and experience progress.

World / Map Commands

These commands control world navigation and location management.

map

Creates an inline location menu where each item has a label and an associated command. When the player selects an item, the corresponding command is executed. The map block must be closed with endmap.

genmap

Generates a randomized world map by selecting locations from a built-in set of location names. The generated map is stored internally and used by the worldmap command.

worldmap

Displays the generated world map as a navigable menu. The player can select a location to travel to, save the game, or exit the story. Locations are created using genmap before worldmap is called.

teleport

Moves execution directly to a labeled location in the script. This is equivalent to goto but uses destination-style naming to indicate movement within the story world.

Combat System

These commands implement turn-based combat encounters between the player and enemies.

combat

Starts a turn-based combat encounter. The enemy name, hit points, minimum damage, and maximum damage are provided as arguments. During combat the player can attack, use a potion from their inventory, or attempt to run. The result of the encounter is stored so it can be checked afterward.

Journal System

Journal commands allow the story to store narrative notes, discoveries, or lore entries.

journaladd

Adds an entry to the journal under a named key. The first argument is the key name and the remaining text is the entry content. If an entry with the same key already exists it will be overwritten.

journal

Displays all stored journal entries in a dialog.

Save System

These commands store and restore player progress.

save

Stores the current game state.

load

Loads a previously saved game state.

checkpoint

Saves the current game state, identical to the save command. Useful as a semantic marker in scripts to indicate an intended save point rather than a player-triggered save.

Script Import

@folder

Loads additional script content from a specified subfolder.

Program Exit

exit

Stops execution of the current story and closes the interpreter.

Language Features

StoryBuilder is a lightweight scripting language designed for building interactive audio stories, games, and narrative systems. The language focuses on readability, accessibility, and flexibility while still supporting structured programming concepts.
Scripts are executed line by line by the Story interpreter. Each command performs a specific action such as displaying dialog, playing sounds, manipulating variables, or controlling story flow.
The language supports the following core features.

Variables

Variables allow scripts to store and manipulate information during execution. They can contain numbers, text, or values returned from other commands.
Variables can be created using commands such as var, set, and write, and can be referenced inside text or commands using angle bracket notation.

Variables are commonly used for

storing player input
tracking story state
storing random results
controlling conditional logic
passing values to functions

Variables can also be modified with arithmetic commands such as add, sub, mul, and div.

Arrays

Arrays store lists of values that can be used for menus, random selections, or structured data.
Arrays can be created manually or generated automatically using commands like array, or range.

Arrays are commonly used for

menu options
random selection systems
procedural content generation
storing collections of items or locations

Array manipulation commands allow values to be added, removed, shuffled, sorted, or filtered.

Functions

Functions allow reusable blocks of script logic to be defined and executed when needed.
Functions help organize large scripts and eliminate repeated code.
A function can contain any valid script commands, including loops, conditionals, menus, and audio playback.
Functions may accept arguments, which become local variables available inside the function body.
Variables created inside functions remain local to that function and do not interfere with other parts of the script.
Execution returns to the calling location when the function finishes or when the return command is used.
When calling a function, multi-word arguments must be wrapped in quotes to be treated as a single value. Without quotes, each word is passed as a separate argument.

Functions are ideal for

reusable gameplay mechanics
mini-games
repeating story events
combat logic
inventory systems

Loops

Loop commands allow scripts to repeat sections of logic automatically.
StoryBuilder supports several loop types, including while, for, foreach, and repeat.

Loops can be used to

validate player input
process arrays
repeat gameplay actions
simulate animations or timed systems

Loops support the break and continue commands for advanced control over loop behavior.
Break and continue work correctly when placed directly inside a loop body. However, they do not work correctly when placed inside an if block that is nested inside a loop. In that case, use goto with a label to jump back to the top of the loop or forward past it instead.

Conditional Logic

Conditional commands allow scripts to make decisions based on variables, player actions, or game state.
Using if and else, a story can branch into different outcomes depending on conditions.

Conditional logic is commonly used for

branching story paths
gameplay decisions
inventory checks
quest progression
random events

Random Systems

StoryBuilder includes built-in commands for generating random results.
These commands allow developers to implement game mechanics such as coin flips, dice rolls, random selections, and spinning wheels.

Random systems can be used for

mini-games
procedural storytelling
RPG mechanics
randomized events
decision systems

Audio System

StoryBuilder includes built-in audio support for sound effects, ambient environments, and background music.
Sound commands allow scripts to play audio feedback for actions, environments, and cinematic moments.
Audio can be used to create immersive audio-based gameplay experiences.

Interactive Menus

Menu commands allow players to choose actions, answers, or story paths.
Menus can be generated dynamically from arrays or defined directly inside scripts using structured choice blocks.

Menus are commonly used for

player decisions
branching story paths
selecting gameplay actions
navigating maps or menus

Command Rules

StoryBuilder scripts are executed line by line from top to bottom unless a command changes the flow of execution.
Understanding how commands are processed helps prevent unexpected behavior in scripts.

Sequential Execution

By default, the interpreter reads and executes commands in the order they appear in the script.
After each command runs, the interpreter moves to the next line.
Commands that do not modify execution flow will simply perform their action and allow execution to continue normally.

Flow-Changing Commands

Some commands change the current execution position in the script. These commands override normal sequential execution.

Commands that modify execution flow include

goto
gotoif
call
return
loop commands
conditional logic commands

When these commands are used, execution may jump to another location in the script.

Labels

Labels mark specific locations in the script that execution can jump to using commands such as goto.
Labels do not execute any code themselves and exist only as reference points.
Because labels allow unrestricted jumping within the script, they should be used carefully. Excessive label usage can make scripts difficult to follow and maintain.
In many cases, functions and loops provide a more structured alternative to label-based control flow.

Functions and Structured Flow

Functions provide a structured way to organize reusable script logic without relying heavily on labels.
When a function is called, execution jumps to the function definition and runs the commands inside the function.
Once the function finishes or a return command is reached, execution resumes at the point where the function was called.
Using functions instead of label jumps helps keep scripts easier to read and maintain.

Loop Blocks

Loop commands define a block of commands that repeat automatically.
Execution enters the loop and continues running commands inside the block until the loop condition ends or a control command exits the loop.
Loop structures must always be properly closed using their matching end commands.

Input Commands

Commands that request input from the player pause script execution until the player responds.
If the player cancels the input, the script may exit the current loop or return to the previous menu depending on how the script handles the result.

Command Blocks

Some commands create multi-line command blocks that must be closed with a corresponding ending command.
Examples include loops, functions, and structured choices.
These blocks allow complex logic structures to be written clearly and safely.

Script Structure

A typical StoryBuilder script follows this structure

Story setup and introduction
Variable or array initialization
Player interaction through menus or input
Game logic using loops, conditions, and functions
Story progression and branching
Ending or exit point

Organizing scripts this way helps keep stories readable and easier to maintain.

Best Practices for Writing Scripts

Writing clear and well-structured scripts helps prevent errors and makes stories easier to expand or maintain later. The following recommendations will help authors create stable and readable StoryBuilder projects.

Use Functions for Reusable Logic

Functions are the preferred way to organize reusable script logic. Instead of copying the same sequence of commands multiple times, place the logic inside a function and call it whenever needed.
Functions improve script readability and reduce duplication. They are ideal for gameplay systems, mini-games, reusable menus, or repeated story events.

Use Variables to Track Game State

Variables allow scripts to store and track important information such as player decisions, inventory counts, or random outcomes.

When referencing variables inside commands that output or use values (such as text, wait, play, or math expressions), wrap the variable name in angle brackets like <varname>.
When using variables in conditions or control flow statements such as if, while, or elseif, use the variable name directly without angle brackets.

Keeping important values stored in variables makes scripts easier to manage and allows the story to respond dynamically to player actions.

Use Arrays for Lists and Menus

Arrays provide a clean way to manage lists of values such as menu options, world locations, or item collections.
Using arrays with menu commands allows scripts to dynamically generate menus or random selections without rewriting the script each time the content changes.

Prefer Structured Loops Over Labels

Loop commands such as while, for, foreach, and repeat should be used when repeating logic.
Loops make scripts easier to understand than repeatedly jumping between labels. They also provide built-in commands such as break and continue to safely control loop execution.

Keep Functions Focused

Functions should perform a single task whenever possible. Keeping functions small and focused makes them easier to reuse and debug.
For example, a function may handle a combat turn, inventory check, or puzzle system without mixing unrelated logic.

Organize Scripts Into Logical Sections

Large scripts are easier to maintain when organized into sections such as

story introduction
system initialization
gameplay mechanics
reusable functions
story events
ending or cleanup logic

Clear structure helps prevent confusion as the story grows.

Use Clear Variable Names

Variables should be named in a way that clearly describes their purpose.
Clear names make scripts easier to read and help prevent mistakes when scripts become large.

Use Random Systems Carefully

Random commands such as dice rolls, coin flips, or wheel spins should be used in ways that enhance the story rather than create unpredictable or confusing outcomes.
Random systems work best when they influence gameplay mechanics, mini-games, or optional story variations.

Common Mistakes and How to Avoid Them

Even simple scripts can produce unexpected behavior if commands are placed incorrectly or execution flow is misunderstood. The following tips describe common mistakes and how to prevent them.

Placing Executable Commands Before Story Setup

Scripts are executed line by line from the beginning. If commands that request player input or run gameplay systems appear before the introduction or setup text, those commands may run immediately.
To avoid this, place introductory story text or setup logic at the start of the script.

Using Too Many Labels

Labels allow scripts to jump to different locations, but excessive use of labels can make scripts difficult to follow.
Whenever possible, use structured commands such as functions, loops, or menus instead of jumping between many labels.

Close Command Blocks

Commands that create blocks of logic must always be closed properly.
Examples include loops, functions, and structured menu blocks. Forgetting to close these blocks can cause unexpected script behavior.

Infinite Loops

Loops that never change their conditions can run forever.
Ensure that variables controlling loops are updated properly or include break conditions to exit loops when appropriate.

Overwriting Important Variables

Using the same variable name for multiple purposes can lead to unexpected results.
Local variables inside functions help prevent this issue by isolating values within the function.

Handling Player Cancellation

Input commands allow players to cancel prompts. Scripts should be prepared to handle canceled input so that the story can return to a menu or exit gracefully.
Handling cancellation properly prevents scripts from becoming stuck or behaving unpredictably.

Misplacing Flow Control Commands

Commands that change execution flow should be used carefully. Placing them incorrectly can cause sections of the script to be skipped or repeated unintentionally.
Understanding how execution moves through the script helps avoid these issues.

Testing Script Branches

Interactive stories often contain many possible paths. Each branch should be tested to ensure that the story continues correctly no matter which option the player selects.
Testing different paths helps identify logic errors before release.

Final Note

StoryBuilder is designed to make interactive storytelling accessible while still supporting powerful scripting features. By organizing scripts carefully and using structured commands such as functions, loops, and arrays, authors can create complex narrative experiences while keeping scripts readable and maintainable.

Script File Structure

StoryBuilder organizes stories using a simple folder-based structure. Each story is stored inside its own directory containing the script file and any associated audio assets.
This structure allows stories to remain self-contained and easy to distribute.

Story Directory

All stories are stored inside the main stories directory.

Each individual story has its own folder inside this directory.

Example

data/stories/my_story/

The folder name becomes the story identifier used by the engine.

Main Story Script

Each story must include a main script file that contains the commands used by the interpreter.

data/stories/storyname/info.dat

This file contains the entire script for the story, including narrative text, gameplay logic, menus, and commands.
When a story is selected, StoryBuilder loads this file and begins executing the script from the top.

Asset Directory

Stories can include optional audio assets that are used by sound commands during gameplay.
All assets for a story are stored in an assets folder within the story directory.

Inside this folder, assets are organized into categories.

Sound Effects

Short sound effects such as clicks, game actions, or environment sounds are stored in the misc directory.

These sounds are typically used by commands such as

play
cutplay
random event systems
mini-games

Ambient Sounds

Looping environmental sounds are stored in the source directory.

These sounds are used to create background environments such as wind, rain, machinery, or crowd noise.
Ambient sounds are typically played using the amb command.

Music

Background music tracks are stored in the music directory.
Music tracks are designed to loop continuously and are played using the mus command.

Additional Script Files

StoryBuilder also allows scripts to load additional script content from subfolders using the script import command.
This makes it possible to organize large stories into multiple files or modules.

For example, a story may separate its combat systems, puzzles, or mini-games into their own script folders.

Asset Naming

Audio files should be named clearly so they can be referenced easily within the script.
File names are used by sound commands to locate the correct asset inside the story folder.
Using consistent naming conventions helps keep large stories organized.

Story Distribution

Because each story exists inside its own folder, distributing stories is very simple.

To share a story, the entire story folder can be copied and placed inside the data/stories directory of another StoryBuilder installation.
Once added, the story will automatically appear in the story selection menu.

Summary

The folder structure used by StoryBuilder keeps stories organized and self-contained. Each story includes its script and assets in one location, making it easy to develop, test, and distribute interactive stories without modifying the core application.
