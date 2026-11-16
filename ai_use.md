# AI Use

Generative AI used: Yes

If no group member used AI, no entries are needed. Otherwise add an entry for each substantive use, including assistance with code, design, debugging, documentation or videos.

## Entry 1

- Member and date: Minh 16 Oct 2026
- Tool and model/version, where available: Gemini free plan
- Purpose: Brainstorming ideas for ambiguous in-game items and generating initial ambiguous item descriptions to fit the game’s narrative.
- Relevant prompts and outputs used, or retained transcript location:
Prompt: "Generate me a set of ambiguous items that can be interpreted as evidence of your partner’s secret (such as an affair or a gambling addiction)” 
Output: Generated a list of ambiguous item concepts and draft flavor text/descriptions for each item.
- Files/materials affected: The original script
- What we kept, changed or rejected: The overall game structure and both acts were written entirely manually with minimal AI assistance. From the AI output, we kept a few concepts for items that fit the structure, rejected some and rewrote most of the item’s description to match the game’s tone
- How we checked it; tests and corrections: Play tested and reviewed the game, trying out all the different endings to make sure that all the descriptions fits the general vibe of the game and that there’s no weird AI-phrasing.

## Entry 2

- Member and date: Minh Oct 20
- Tool and model/version, where available: Gemini 
- Purpose: Minimal assistance in refining and polishing specific lines of dialogue that had already been drafted manually
- Relevant prompts and outputs used, or retained transcript location:
Prompt: "Here is my drafted dialogue for the partner’s reaction to each item. Can you help me alter some of the wording so that it feels more natural and realistic instead of feeling corny and forced.
Output: Gave out minor rephrasing for a few lines of dialogues and provided more ideas which in turn helped us rewrite a few things 
- Files/materials affected: The script
- What we kept, changed or rejected: The majority of the dialogue was written by hand from the limited AI suggestion, adopted a few rephrasing for a better flow, rejected complete rewrites.
- How we checked it; Playtesting and reading through the full script in context to make sure that the dialogue sounds natural and the character’s feel is consistent.




## Entry 3

- Member and date: Siranat 22 Oct 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Design a system for Pixelart and render it and show it on the screen.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: If I were to turn the game into a pixelart style how would I go about that? 
Output: Claude gave us functions to draw the art using upper half block “▀” characters and load_png(), paeth() function along with paste(), to show the picture on the terminal. (Summary)
 - Files/materials affected: main.py
- What we kept, changed or rejected: We kept the system of drawing with half block but we later discovered that drawing with the upper half block ▀ is visually buggy on Mac terminal because it is a shorter than normal so we had to do a little fix around and change the character to ▄ which fixes the visual problem on mac terminal.
- How we checked it; tests and corrections: We ran the game on both VScode terminal and native terminals to see if they react normally, when it did not we observe how is it faulty and asked the AI for possibilities and make decisions

## Entry 4

- Member and date: Siranat 5 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Add a frame to the game to show the border, and design some missing arts, and also design a new framework for the game progressing (pressing button to process).
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: Could you add a border to the game and also design a structure to develop the game furthermore? I’d prefer if the area and clues are tied together in something like a dictionary or list so i can call them to use like closet[guilty] and it would show the correct item. Can you also design the art for some of the missing art.
Output: Claude gave us art for the bedroom, hallway, partner’s faces, a structure for areas and clues searching
 - Files/materials affected: main.py, /art/ folder where the art of the game is kept.
- What we kept, changed or rejected: We kept the structure and some of the art claude gave us, some of the art just did not look right we had to change it ourselves. The structure claude provided us really sped up the progress of the game development since it allows us to build the game like lego with building blocks.
- How we checked it; tests and corrections: We ran the game to see if what we modified using the structure frame work correctly or not, if it doesnt we check the log and see why usually its a syntax error. The frame that claude gave us to use as a border works fine, the art had to change a little.

## Entry 5

- Member and date: Siranat 12 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Fill in the missing art e.g the betting slip, wedding ring screen, etc.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: Could you add the missing art that can be seen in the main.py? Currently i just leave the screen empty when the missing art is called.
Output: Claude gave us art for the betting slip, pawn ticket, letter, ring, paperback, takeout menu, cat videos and flip-flop.
 - Files/materials affected: /art/ a folder containing every art used in the game.
- What we kept, changed or rejected: We kept most of the art claude provided us but still as an AI generated art, some of them didn’t look right, we had to change the art for betting slip and pawn ticket.
- How we checked it; tests and corrections: We ran the game to see if the art make sense or not. If it doesn’t we just Pixilart application to draw the art which doesn’t take long.

## Entry 6

- Member and date: Siranat 15 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Adding extra dialogue to the item or scene.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: If I were to add another dialogue while staying in the same screen how would I go about that?
Output: Claude told me to do a for loop for the item checking if the description of the item in the list had “more:...”  in it or not if it does show the text while still using the same code for showing the background, creating the illusion that we are still in the same exact scene.
 - Files/materials affected: main.py
- What we kept, changed or rejected: We kept the idea of using a for loop to check if the item in the entry had more information in it or not but we changed “more:...” to [more:...] to turn it into a list because for loop would just call up the text character by character if it was a string.
- How we checked it; tests and corrections: We tried running the game again and when we get to the item with “more” in the entries we process to see if the more actually showed up or not, at first attempt the “more” section just showed up letter by letter, because it is treated as a string, and in for loop a string get looped character by character we just had to change “more:..” to [more:....]

## Entry 7

- Member and date: Siranat 15 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Design a diagram of the how game progress, the structure of it.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: If I were to make demo/technical video on the game to explain it and what we implemented how would I go about that? Maybe a diagram of it to explain the basics idea of the game? (I also pasted the rubric of the project on this so it knows what to explain)
Output: Claude gave me a diagram of the game structure, and also a timeline for the demo video like what to explain and when to explain it.
 - Files/materials affected: None.
- What we kept, changed or rejected: We rejected it as it didn’t seem natural, and the game was quite simple enough that we didn’t need a diagram for it.
- How we checked it; tests and corrections: We took a look at it and thought that it is quite a little bit extreme and isn’t that necessary.

Keep evidence accessible to the teaching team. Remove credentials and unrelated personal information. Submit the completed file as `ai_use.md` with the project.

## Entry 8

- Member and date: Siranat 15 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Design a diagram of the how game progress, the structure of it.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: If I were to make demo/technical video on the game to explain it and what we implemented how would I go about that? Maybe a diagram of it to explain the basics idea of the game? (I also pasted the rubric of the project on this, so it knows what to explain)
Output: Claude gave me a diagram of the game structure, and also a timeline for the demo video like what to explain and when to explain it.
 - Files/materials affected: None.
- What we kept, changed or rejected: We rejected it as it didn’t seem natural, and the game was quite simple enough that we didn’t need a diagram for it.
- How we checked it; tests and corrections: We took a look at it and thought that it is quite a little bit extreme and isn’t that necessary.

## Entry 9

- Member and date: Siranat 16 Nov 2026
- Tool and model/version, where available: Claude Opus 5.5
- Purpose: Fixing terminal sizing problem.
- Relevant prompts and outputs used, or retained transcript location: 
Prompt: Right now when the terminal is smaller than 80x24 the game doesn't start when you run the command, which is correct, but after resizing it it to be big enough, the terminal got bricked, even pressing ctrl+c doesn't kill the python command. Could you make it so that player get an option to either quit the game so the code stop itself and make it so that if the terminal size is adequate make the game continue immediately.
Output: Claude gave me functions to get the current terminal size, and functions to send a message when the terminal is too small and keep checking if thet terminal is big enough or not if it is, show the game.
 - Files/materials affected: main.py
- What we kept, changed or rejected: We kept the functions claude gave us to fix the terminal sizing problem
- How we checked it; tests and corrections: We ran the game again this time starting with terminal too small, the game doesn't start with it, you can press q to quit or fix the terminal size and the game would pop up.




Keep evidence accessible to the teaching team. Remove credentials and unrelated personal information. Submit the completed file as `ai_use.md` with the project.


