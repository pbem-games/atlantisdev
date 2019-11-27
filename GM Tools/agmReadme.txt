
To follow is Larry Stanbery's documentation of his AGM software.  I'm
uploading this Readme file for two reasons:  (1) to allow others to
read his documentation *before* downloading and running his
installation program, and (2) to present a work-around for a known bug
in his program.  I have not modified his documentation in any way,
shape or form.  I've only prefaced it with this introduction.

To start a new game of Atlantis, you cannot specify a turn number of -1
as given in the documentation below.  Instead, follow these steps:

  (step 1) create a directory named "turn000" in the root game
	     directory, e.g., "mkdir turn000"

  (step 2) execute "atlantis new" in the "turn000" directory

  (step 3) in the "turn000" directory, copy "game.out" to "game.in",
           e.g., "copy game.out game.in"

  (step 4) in the "turn000" directory, copy "players.out" to
           "players.in", e.g., "copy players.out players.in"

  (step 5) run AGM for the first time, and configure the program as
           described in Larry Stanbery's documentation below.  SET THE
           TURN NUMBER TO "0", NOT "-1".

That's the work-around.  And now here's Larry Stanbery's documentation
in its entirety *without* modification: 

========================================================================

Atlantis Game Master (AGM)
Copyright (C) 1999 Larry Stanbery
All Rights Reserved.

------------------------------------------------------------------------

Table of Contents

1. Introduction
2. Usage
2.1. Configuration
2.1.1. Basic Configuration
2.1.2. Advanced Configuration
2.2. Running your game
2.2.1. "Factions"
2.2.2. "Run Checks"
2.2.3. "Run Turn"
2.2.4. "Gen Factions"
2.2.5. "Gen Times"
2.2.6. Times Note
2.2.7. Mail Log
3. Email Commands
3.1. Notation
3.2. Orders
3.3. Times
3.4. Rumor
3.5. Create
3.6. Resend
3.7. Remind
3.8. Delete
4. Comments, License

------------------------------------------------------------------------

1. Introduction

The Atlantis Game Master (AGM) was designed for those folks who are
running, or are planning to run, Atlantis under some Microsoft Windows
platform.  Configure it with information about your game -- the turn
directory, the executable file, your mail host, etc. -- and it will
help you by running the game for you.  All you need to do is ensure you
have an email account which receives only Atlantis orders -- all other
mail will be junked (saved in a text file).

------------------------------------------------------------------------

2. Usage

2.1.  Configuration

2.1.1.  Basic Configuration

When you first run the AGM, you want to click the "Configure" button.
This is the place where you enter all the information about your game,
your mail server, etc.  There are two possible scenarios:

A -- You're starting a brand-new game, and haven't even created the
     world.

A.1.  Start the AGM.  Click the "Configure" button.
A.2.  Enter the data for your game's name, email address, mail hosts,
      base turn directory and program.  Make sure that the "Turn number"
      is set to -1.  (This special state will run your game with the "new"
      option, so it will prompt you for the size of the world, and then
      it will create the world.)
      Click "OK" when finished.
A.3.  Click the "Run Turn" button.  You will be prompted for the size of
      your world.
      Your new world will be saved in the "turn000" directory under your
      "base turn directory".
A.4.  Your game should be ready.

OR

B -- You're already running a game, and wish to use the AGM.

B.1.  Start the AGM.  Click the "Configure" button.
B.2.  Enter the data for your game.  Set the "Turn number" field to the
      current turn number for your game.  The AGM expects turn
      directories to be named "turnXXX", XXX being the turn number
      (left-padded with zeros).  Historical data is not necessary --
      just data for the current turn.  So, if it is turn 5, make sure
      you have a directory called "turn005", with the "game.in" and
      "players.in" files in it.
      (Make sure you don't have "report.*" files or "game.out" or
      "players.out" files, since they will prevent the proper execution
      of the coming turn.)
      Click "OK" when finished.
B.3.  The AGM should be ready for use.

2.1.2.  Advanced Configuration

There is more to a game than just submitting orders, right?  You have to
be able to add new players, and you may want to publish a Times, to
which the players can contribute.  These items are additional
configuration parameters which you can set.  On the "Game Info" tab of
Configuration, you can select whether new factions can be created by
email, and whether to use the Times option (and, additionally, whether
Rumors in the Times will provide a Times Reward).

In order to use the Times option, you must include some source code in
your game executable.  The source code is in the file "mods.txt".  Add
it, and you'll be in business.  Please note -- you'll also need to set
the global TIMES_REWARD variable in rules.cpp to some positive value.

2.2. Running your game

Once you've configured the AGM, you should be able to use it to take
care of the mundane tasks of the game, leaving you with time to do
whatever it is you do.

2.2.1  "Factions"

The "Factions" button is used for faction maintenance.  It displays
a list of all factions in the "players.in" file.  The fields on the
right show the details for the selected faction.  You can modify these
values by typing in the fields and "Apply"ing them.  If you select a
faction from the list, without "Apply"ing your changes, your changes
will be lost.

The "Apply All" buttons next to "Times Reward", "Send Times", and
"Reward" will apply the value you've set to all factions.  You'll
be prompted to make sure you wish to do this.  Additionally, the
change can be limited to established factions, so that new factions
won't get a reward for something that they couldn't have participated
in.

Once you've made changes, you can "Save" them, which will overwrite
your "players.in" file.

You can even create a new faction manually, by entering data in the
fields, and "Add"ing the new faction.

If, for some reason, the turn report or Times for a faction wasn't
sent, and you wish to send it (rather than the player initiating
a request), you can click the "Send Report" or "Send Times" button.

Of course, when you're finished with your viewing and/or changes, you
can "Close" the window.

2.2.2 "Run Checks"

When you click the "Run Checks" button, it will check your email for
orders.  Anything that doesn't appear to be orders will be saved as
a file named "junk.XXX", XXX being a number.  Additionally, any
attachments to email messages will be placed in the "base turn
directory" (so you can handle the fact that someone attached
their orders).

Orders are saved in the current turn directory, run through the game
to check syntax, and the results of the check are emailed back to the
player.

2.2.3.  "Run Turn"

"Run Turn" will run the game engine with the "run" parameter, which
produces the turn reports.  First, it checks the email one last time
for any "stragglers".  (You'll be prompted about this, just in case
you checked orders earlier, and don't want to recheck after the
deadline.)  After that finishes, the AGM will mail out turn reports.
If you've turned on Times, the AGM will then mail out the Times.
The final step:  the AGM creates the directory for the next turn,
copies over the "game.out" and "players.out" files, as the "*.in"
files.

An extra product of the "Run Turn" is a file named "factions.txt",
in the directory of the turn just run.  This list can be placed
on a Web page, or emailed to players -- it is an extract of the
"players.out" file, which shows the name of a faction, its number,
and the email address of the faction.  (This is used by AtMap.)

2.2.4. "Gen Factions"

If, for some reason, the execution of "Run Turn" stops, and it
doesn't create the "factions.txt" file, you can click "Gen Factions"
to remedy it.

2.2.5. "Gen Times"

Similarly, if the Times isn't created, you can click "Gen Times"
to create it.

2.2.6. Times Note

As the GM, you can include a note in the Times whenever you wish.
Create a file named "times.0" (times dot zero) in the turn directory.
The file is plain text, and will appear as a Times article from
Administrator (0).

2.2.7. Mail Log

As a useful aid to you, every email that is received is logged in
a file named "maillog.txt" in the current turn directory.  If a player
complains that someone's stolen his password, and has submitted orders
for him, you'll be able to see the evidence of this in the Mail Log.

------------------------------------------------------------------------

3. Email Commands

At this point, you're probably wondering what commands are available,
and how they're used.

3.1. Notation

The following notation is used:
<x> -- x is a required item
"x" -- x is a quoted string
[x] -- x is an optional item
|   -- acts as "OR" (x | y means x or y)

3.2. Orders

#atlantis <faction number> ["password" | password]
[orders]
#end

This, of course, is the standard Atlantis orders command.  If the
password is valid, the #atlantis line to the #end line will be saved
as "orders.<faction number>" in the current turn directory.

3.3. Times

#times <faction number> ["password" | password]
[body of Times article]
#end

The structure of this is identical to that of the Orders command.
The text of the article is unprocessed.  If the password is valid,
the body of the article (minus #times and #end) is saved as
"times.<faction number>" in the current turn directory.

3.4. Rumor

#rumor <faction number> ["password" | password]
[body of rumor]
#end

This works identical to Times.  The body is saved as
"rumor.<faction number>".  Additionally, the faction number is added
to the "rumors.txt" file in the curent turn directory.

3.5. Create

#create "faction name" "password"

The quotes are mandatory.  The email used to send the request is
used as the faction's email.  An entry in "players.in" will be
added to create the new faction turn the next turn.

This won't run if you've turned off the option to create new factions.

3.6. Resend

#resend <faction number> ["password" | password]

This command will look for last turn's report and send it to the player.
It sends it to the address of record, not the requestor.  Of course,
it only works if the password is right.

3.7. Remind

#remind <faction number> ["password" | password]

This command will send the current turn's orders to the address of
record.  This is useful if you've forgotten what orders you sent.

3.8. Delete

#delete <faction number> ["password" | password]

This command will delete the current Times and rumor for the faction.
Of course, you could always submit a new Times and rumor to overwrite
your existing articles.

------------------------------------------------------------------------

4. Comments, License

This software is distributed AS-IS, without warranty, expressed or implied.
I suppose I should GNU CopyLeft it -- I'll look into it.

You may not distribute this software without my permission.  (Again, this
may change if I CopyLeft.)

You can contact me at:

stanbery@earthling.net

if you have problems, suggestions, etc.
