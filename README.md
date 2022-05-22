# modsbox.com
My website that I am currently using to display Reversle. The goal of Reversle, my exhibition (pretty much a science fair) project, was to reverse engineer the open source code of Wordle and create new variants of the game. Along with it, a major focus was that exhibition attendees would easily be able to interact with my project by playing it on the website or by scanning the QR codes on my trifold board. Most of the word length modifications and the infinite word function can be found in around lines 950-1000 of the code.

Disclaimer about Originality:
-----

I am not claiming that this is my own intellectual property, for I simply modified the existing open source code for the original Wordle website (I obtained the code before the site was bought by The New York Times)

Special thanks to the developers and owners of the original game, for this project wouldn't have been possible without their original code. 

Why I chose this Project:
-----
I decided to do this project for four main reasons. 

1. I wanted to try it out for myself:
I learned that software engineers were obtaining the code of the game and modifying it to create their own variants, and I was curious as to whether or not I could learn about the design of the game and accomplish this as well (even though I lack experience with JavaScript).

2. It provided a goal for my programming:
I have been interested in creating a website with a specific function for a while, but I lacked a defined goal for exactly what I wanted to create. This idea gave me the defined goal that I was searching for, since the simple goal was just “reverse engineer the game to create a new variant”.

3. Interactivity:
In order to make my project stand out from the others, I wanted viewers of it to be able to interact with it instead of simply learning about it. Overall, people tend to enjoy discovering information about new topics (ex: web design, software engineering, and the design of the program) by interacting with a product, instead of listening to a person trying to explain the foreign concept. Also, for people that were uninterested by the overly complicated projects, they would be able to walk up to mine in order to mess around on these games, but then they would become intrigued by the creation of the project.

4. Familiarity:
With this project, a majority of people already possess existing knowledge about Wordle. So, it was much less difficult to educate them about the design process, since they already possess a general idea of what the project “does”. In addition, this familiarity makes it much less difficult for a person to approach me and ask questions about it. After all, would you rather  learn about this or a complex physics concept that takes a long time to explain to the average person?

So yeah, those are basically the four contributing factors for my decision to reverse-engineer Wordle as my project.

Challenges:
-----

Throughout this project, I had to overcome numerous challenges in order to reverse engineer and create these new programs. Here are some of the main issues that I faced in the creation of this project:

-Finding a way to obtain and modify the files of Wordle’s source code
-Searching through over 2000 lines of code in order to find and edit important sections of the program for my reverse engineering process
-Learning how the game organizes the position and amount of rows
-Figuring out the method to changing the amount of letters for a game
-Changing the amount of inputtable boxes displayed in the game (spaces to insert letters)
-Editing and reformatting the “la” dictionary (possible answers) and the “ta” dictionary (inputtable answers) multiple times
-Removing the daily word function from the game and creating the new infinite word function.
-Modifying the text and colors to become different for each of my newly created variants
-Struggling to learn how to use JavaScript, a new programming language for me, as I tried to dissect this project (I’m most experienced with Swift, HTML, and C#)
-Creating a running host website for the project that contains links to each individual version of the game

Steps to Obtaining the Files:
-----

In chrome, go to the original website: powerlanguage.co.uk 
Go to the file menu and select Save Page As…  then select the default option of web page.complete
From there, that will create an HTML file of the game on desktop that can be used to play the game offline. In addition, it will create a directory of files including a JavaScript library and a main.js file that contains the code of the game.
Upon opening the main.js file, it becomes apparent that it’s impossible to read because the entire code is on a single line.
From this point, in order to create a file that can be read and reverse engineered, one must “beautify” the file. For this, I used a website called: beautifier.io
Then, copy and paste the main.js file into the website. Once it’s pasted in, press the “beautify.code” button. 
By pressing this button, the file becomes beautified to the point that it can easily be modified.
Finally, with this new beautified file, replace the original code in main.js with the new version. Now, we have a fully editable .html file and a fully editable .js file to use in this process.

Editing the Wordle Dictionaries:
-----

In order to successfully change the number of letters in a Wordle game, I had to take two major steps. First of all, I was forced to edit a variety of variables and functions in order to remove or add characters. Although this took a while, I was eventually able to figure out Wordle’s letter input system via trial and error through editing lines of code. However, the second step quickly proved to be a momentous task. In this next step, I was going to have to edit the entire Wordle dictionary in order to include words with a different number of letters. 

For this task, I started off by creating the dictionary for Fourdle (a four letter version of the game). Initially, I searched for a list of English words in a .txt file, and I ended up finding one file on GitHub after a few minutes of searching: 

https://github.com/dwyl/english-words/blob/master/words_alpha.txt

However, this list of English words included words of all character lengths. So, for Fourdle, I had to find a way to filter out all of the four letter words from the rest of the words in the file.  By searching through Stack Overflow (a commonly-used coding Q&A website), I learned of the ‘grep’ command on Mac, which performs the exact function that I needed. Here is the function below:

grep -o -w '\w\{(insert number of letters)\}' (insert file name).txt


Now the words needed to be captured into a file, so I can eventually get it into the needed format for Fourdle. This format is a long javascript text array defined as a variable in the format of:

var wordlist: { "word1", "word2", ... };

After more research, I learned that by using the '>' symbol, it's possible to capture the output in the console to a file. So I just had to do this to get it into a file:

grep -o -w '\w\{4\}' words_alpha.txt > 4letterwords.txt

With this command, I had now gained a file with one word in each line:

[1] Word1
[2] Word2
[3] Word3

But now, in order to fit the list into the variable, the words have to all be surrounded by quotes with a comma and space afterwards (as demonstrated by the var wordlist format). Thankfully, there’s a website that allows for a person to do this by simply attaching the .txt file: 

https://commaquote.azurewebsites.net/

After this tedious process, I finally had the dictionary section finished. Or so I thought….There was one problem remaining. It turns out that Wordle has two dictionaries. One large dictionary for all inputable words, and another small for potential Wordle answers (common words). This is because a variety of words in the dictionary are unknown and unlikely to be guessed by the average person. So, now I had to figure out a way to get four letter common words. For a while, I lacked a solution. I tried searching the words that I had added into the Fourdle dictionary and filtering out uncommon words, but there were thousands of these words to go through. Eventually, it hit me: I need to search on GitHub. So, I ended up scrolling through a few pages before finding a list of the 1000 most common English words on a .txt file:

https://gist.github.com/deekayen/4148741

With this file downloaded on my computer, I proceeded to repeat the entire process of filtering and formatting four letter words. In the end, I had obtained and inputted 327 potential answers for Fourdle. Once this was finished, I had successfully constructed the beta of Fourdle. 

Also, I wanted to create two more variants of Wordle (one with state abbreviations and one with six letters). For the state abbreviations version (State-le), I simply inserted all of the state abbreviations for the inputtable words and the potential answers in the variables. Then, I wanted to make Sixle (six letter Wordle). Thankfully, I was able to repeat the exact steps for Fourdle in order to make this version’s dictionary in a more timely manner. 

Acknowledgements:
-----

As I created this project, I used a variety of online resources in order to simplify the process. First of all, Sublime Text, a source code editor, was extremely helpful throughout the entire reverse engineering procedure, for it allowed me to easily create, modify, and compare the JavaScript and HTML files of this project. In addition, beautify.io was a beneficial website that allowed me to straightforwardly convert the original main.js file into an editable file. Next, I would like to acknowledge GitHub and it’s variety of contributors because this site allowed me to obtain a list of dictionary words and commonly used words in .txt files. Also, commaquote.azurewebsites.net allowed me to easily modify these .txt files to fit into the JavaScript array of strings format. Furthermore, Stack Overflow was an amazing forum that allowed for me to quickly gain assistance with issues that occurred throughout the project. Finally, I must express my greatest appreciation towards the creators of Wordle because I wouldn’t have been able to reverse engineer the game without their impressive website and source code. 
