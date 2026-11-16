# ENGG1330Tut

README

Names: Ayumi Seki, Nguyen Trong Anh Minh
Subclass: D
Container version: Debian Linux 12 (Bookworm) (The provided docker container)
Run command:  python main.py
Tests and known limitations: 

Test: Played the game on both Windows and Mac terminal to ensure the graphics of the game still functions, even if they run on docker some of the graphics may change based on the OS. 

Known Limitations: Doesn’t work on Windows terminal without docker, as two of the libraries used were tty and termios ( which are standard python libraries ), however it works fine within the provided docker.

Contributions: 
Ayumi - First worked on the outline for act 2 of the game, where I wrote the dialogues for the player and the partner during the confrontation. Worked on re-designing the pixel arts for the background, items, and partner’s face since the AI generated ones were looking weird. The size didn’t match the terminal size and some of the items were unrecognizable. Also, I tidied up the codes and removed functions that were not necessary, such as those that were used to catch mistakes during testing, functions that were used only once and hence didn’t need to be functions, etc. For example, we had a check_size function and load_background function to check whether all the images were the right size (80x44 pixels) and stop the game if not. This was useful during testings, but after we were able to run the game without stopping, these were not necessary so I removed them to make the code cleaner. I also contributed by writing the explanations for each functions, which are used for the demo video.

Minh - Came up with the general concept for the game, which is about discovering your partner's affair, which then turned into a secret that can vary, and wrote most of the original script. Drew inspiration from investigation-and-confrontation games like Ace Attorney, leading to a structural split where the first act focuses on searching for items and the second act involves presenting those items to confront your partner. Thought process being that blending emotional relationship tension with classic courtroom mystery mechanics can make a good 2 act game, inducing logical thinking and emotional intelligence for the player. Also created the game's trailer using the game's own assets to showcase the atmosphere and gameplay loop. 

Siranat - Worked on the general coding of the game, the trailer video voiceover, the demo/technical video of the game. Also responsible for debugging the faulty codes that's provided by AI e.g. old mac terminal not functioning properly with true color so we had to change the game to use 8-bit color which is compatible on older mac terminal, fixing the drawing block of the game so the graphics function properly. Also worked on the story of the game e.g the dialogue, the clues, the setting.

Sources: 

The PNG decoding follows the W3C PNG format specification, with help from Claude AI to implement. https://www.w3.org/TR/png/

Functions Definition

1. paeth(a ,b ,c)

It is a function that loads up the png image color, because in png file, the colors come in an matrix of numbers in modulo of 256, and the way it store the number for each position is not traditional, it takes the first position number and then for the neighbor it just store the neighbore value as the difference between that neighbor and the original one, so a RGB color pixel with one neighbor to the right would originally look like:
[[100, 150, 200], [102, 150, 195]]
and when it is encoded it would look like:
[[100, 150, 200], [2, 0, 251]]

basically taking the current value and subtract it with the left neighbor value, if it goes into the negative then we add 256 to it, so 195-200 in the Blue color would be -5+256 = 251

2. load_png(filename)
It calls up the png file, which is saved in rows of RGB (related to the paeth function to correct the colors on this we call up paeth to correct the color in this function, which is why paeth is at the top of the file, the most important one)

3. colour(rgb,ground)
Calls up the colors in rgb in two halves, top and bottom, by using ground we specify which half we wanna color, 38 is for top half and 48 is for bottom half so colour(rgb, 38) would color half top of the pixel

4. paste(picture, sprite, x, y)
Basically pasting the list of list of rgb into the memory of the terminal, the sprite is the item we wanna put into the picture(the terminal) x y is just position on where to put it into the picture

5. scale_up(sprite)
Basically scale up every pixel to be twice as big, works for the clue when we wanna look it up close, like selecting item, when you see it in the inventory list you wanna see normal but when you look into it you wanna see bigger.

6. half_block(top, bottom)
This is what create the game’s pixel it just says what the top should be and what the bottom should be, like red and blue you would get half red half blue, useful for creating  game visual.

7. render_art(picture, rows)
Renders the art that was pasted via the paste function, row tell where to put it, no image is shown on the terminal yet

8. frame_cell(x, row)
Since every art in the terminal is made of text, we need to add the border to the dialouge shown in the game too, otherwise any row with dialouge would be just like a normal text line just black and white occupying rows in the terminal

9. text_row(text, row)
Build line of text, specifying where with the row, and center the text in that row and also call the frame_cell function to draw on the edge of the text so it blends into the game

10. bottom_row(hint)
Just show a single line of text with what to do, like press F to continue, press Enter to start, press any keys,... with background color of yellow and also centered.

11. wrap(text)
Cuts long text into lines so it doesn't go over the frame border

12. get_key()
Read the key that the player presses for other function in the game.

13. key_waiting(seconds)
If no key is pressed during the text rolling out, the text will continue to keep rolling out, but if a key is pressed it will skip to the full text being shown.

14. type_out(lines, first_row)
The function responsible for rolling out the the text character by characters the speed depends on type_speed variable set in the file. It’s als opaired with the key_waiting() to decide whether to roll out the text normally or show the whole text at once, because if the function return false, it skips the entire function and go straight to show function, which erase the screen and draw a new one instantly creating the visual that entire text was shown.

15. show(picture, lines, hint=” “)
This is the most important function to show the visual in the game,it checks whether the terminal is at least 80x24 or not, it draws one big screen calling the render_art function for the background and the text_row, frame_cell, bottom_row, wrap functions to show the text in the game

16. clock(minutes)
A simple function to turn minutes into hour format time like 1290 to 9:30pm

17. ask_menu(picture)
A function after player press F in the press_on function that return player to the menu.

18. press_on(picture, lines, hint=”Press any key  |  F for menu”
A function thats player either press F or any other key, for F, it will call ask_menu function to ask whether they wanna return to menu or not, for any other key it progresses the game.

19. bedroom_picture(seached)
It makes the bedroom picture with the numbers 0-9 “drawn” on it, so the player knows which key searches which spot. It starts with the plain bedroom png (ROOM), then gos through all 10 spots in AREAS. Each spots has its own “tag”, which is the (x, y) coordinate of where the top left corner of the number goes. If the spot’s key is in searched (the set of spots already searched), it pastes the grey number. Else, it pastes yellow one. 

20. closeup_picture(clue)
When you find a clue, it pastes the picture of it in the middle of a spotlight background. Using scale_up, it makes the image twice as big (so 16x16 becomes 32x32) and pastes it onto the spotlight at coordinates (24, 2) which is about the middle.

21. confront_picture(face, holding=None)
It pastes the image of the doorway with the partner standing in it with different faces depending on “face”. If the player is showing them the evidence, it pastes a white card (square background) on the left side at (5, 11), then the item picture on top of the card.

22. meter_line(guilt, paranoia)
It turns the guilt and paranoia numbers into the two bars that is shown during confrontation. Each bar is 10 characters long, and while guilt fills one block per point, paranoia only goes up till 6 before the partner walks out. Hence it is stretched to fill the bar (paranoia x 10 / 6). This is because when paranoia reaches 6, the game ends straight away, but nothing happens on its own when guilt gets high. It only matters during the accusation, therefore has no limit. min(..., METER_SIZE) prevents the bar from going past 10 blocks. It returns a list of multiple (text, color) so that text_row can draw the bars in corresponding colors. 

23. pick_secret()
At the start of every game, this function picks what the partner is hiding. Each secrets has a weight which is the percentage chance of it happening (cheating 32%, planning 21%, unemployed 21%, gambling 21%, nothing 5%). Random.choices picks one secret using these percentage. Since it returns a list even when it only picks one, [0] is added at the end so that the name of the secret is returned as a string.

24. hide_clues(secret)
It decides what item is in the 10 spots before the search begins, based on the secret that was picked with pick_secret(). For each spots, there are two lists, plain and options. Plain contains the harmless clues that fit any secret, while options contains clues to the secret. 85% of the time the spot gets a clue from options, otherwise from plain. Therefore all the clues will either fit the secret or fit any secrets, meaning if the secret is “affair”, a clue that only fit “debt” are never chosen. If there is no secret at all, the chance lowers to 60% instead so that the room still looks suspicious. However, “debt” only has 6 clues and “surprise” and “jobless” have 5 clues that fit the secret, therefore after the random 85% roll, spot that should have had a real clue might have ended up with a harmless one. We added the secrets other than affair after building the entire game, and we only added 5 or 6 clues each so we have added this function. The while loop continues until there are 6 real clues in the found list (spots that got real clues) or the spare list (spots that could’ve got a real clue but didn’t) becomes empty.

25. act_one(secret)
This function basically runs the entire act 1. It first decides what item is at each of the spots before the search begins using hide_clues(secret), so the clues depend on what the partner is actually hiding. It shows the living room and title screen and waits for any key to be pressed with press_on(picture, lines) in order to proceed. Once the player hits a key, the search loop begins. Each search costs 15 minutes, so the player gets 6 searches. With bedroom_picture(searched), the bedroom is redrawn each turn, with searched spots turning to a grey number. Going back to act_one, it then waits for a key to get pressed with get_key(). Here, get_key() is used and not press_on() as press_on() doesn’t tell which key was pressed but just checks for F to return to the menu. Once the player presses a key, the for loop begins. Since the if statement clearly specifies that the key is not in searched, which is a set that includes all the keys that were pressed already, pressing an already-searched number or a random letter does nothing. In the loop, if the spot hasn’t been searched yet, it will be marked as searched and the time goes up by 15 minutes. The evidence is shown and added to the list found. When all 6 searches are done, which means that the time has run out, act_one returns found, which act 2 uses as the evidence the player can show to the partner. 

26. ending(picture, title, story, truth)
Shows the ending screen with title in gold, narration, and truth_line in grey.

27. truth_line(secret)
Looks up what the partner was really hiding and returns it as “The truth: ...”

28. act_two(secret, found)
This function runs the act 2. Guilt and paranoia starts at 0, and clues is a copy of the found list from act 1, so that the clues can be removed from the copied list without changing the original. The while loop runs until the game ends. Each turn, get_key() waits for the player’s choice, F to return to menu, A to accuse, T to let it go, and a number to confront the partner with the corresponding clue. The used clue will be removed from clues with pop so that it can only be shown once. After each confrontation, depending on whether the clue is related to the secret or not, the partner’s reaction changes and the guilt or/and paranoia number increases with replies.get(secret, replies.get(ANY)). If the chosen clue is harmless, replies.get(ANY) is used, which is the annoyed reaction. Once paranoia reaches PARANOIA_MAX which is 6, the game instantly ends with the player losing. Every ending returns True or False, which play() uses to show the win or lose screen.  

29. choose_accusation(face, guilt, paranoia)
When the player chooses to accuse, this shows the accusation menu with 4 secrets options in the options list, where the player picks what they think the partner is hiding. Here, “Nothing” is not an option since you cannot accuse someone of hiding nothing. The while loop and get_key() waits for the player to press a number, and if the player presses a number, it returns that secret’s name.

30. accuse(secret, accused, guilt)
This function decides what happens when the player accuses the partner. If the accusation is right and guilt is 6 or more, the partner convesses and it returns True (win). However if the accusation is right but guilt is too low, the partner denies it and it returns False, because without enough evidence they don’t crack. If the accusationo is wrong, it reveals the truth and returns False.

31. let_it_go(secret)
When the player lets it go, this function is executed. If the partner was hiding nothing or was planning to propose, letting it go was the right choice, so it shows “Best ending!” and the player wins. For any other secret, it returns False which means that the player has lost.

32. play()
It runs the game one after another until the player goes back to the menu. Each game, a new secret is picked with pick_secret() and runs act_one and act_two. 

33. main()
It saves the terminal’s current settings with termios.tcgetattr(fd) and switches the terminal to raw mode with tty.setraw(fd) so that the game reads the keys straight away without pressing Enter. Also sys.stdout.write(HIDE_CURSOR) stops the blinking cursor box. Using get_key(), Enter starts play() and Q breaks out of the loop. The finally block always runs at the end and puts the terminal back to the setting which termios.tcgetattr have saved, clears the screen, and prints the message. Without this, the terminal would stay in raw mode after the game ends which may affect the player’s experience.
