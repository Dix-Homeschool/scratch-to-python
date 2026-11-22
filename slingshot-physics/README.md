# Slingshot Physics: Python Lessons

Nov 22, 2026 · Twelve lessons that take a Scratch slingshot game and rebuild it in Python, with original characters.

## Before you start

**The goal:** rebuild your Scratch slingshot game in Python, one piece at a time. By Lesson 12 you'll have a launcher, a flying character with real gravity, targets to knock over, and levels.

**Art is your choice.** Use whatever characters you like. Draw your own, use characters you already made in Scratch, or draw your own version of the birds. It's your game. There's an optional art break after Lesson 8 if you want your drawings in the game early.

**Setup (do this together, about 20 minutes):**

- Install **Python** from python.org (on Windows, tick "Add Python to PATH"). Then install **VS Code** from code.visualstudio.com and add its **Python extension** from the Extensions icon on the left. To run a file, click the ▶ button in the top-right corner. It works like Scratch's green flag.
- In VS Code, open the Terminal (**Terminal → New Terminal**) and type **pip install pygame** (on a Mac, **pip3 install pygame**). You'll need it starting in Lesson 6.
- Make a folder called **slingshot** to save every lesson file in.
- **Get your own copy of the lessons:** on the lesson repo page, click **Use this template** to make a private copy in your own GitHub account. Then clone that copy into VS Code (**File → Clone Repository**) and save your work there. Each finished lesson is a commit, so you can go back if something breaks. If you don't have a GitHub account yet, skip this step and just make the **slingshot** folder.

**How each lesson works (45 to 60 minutes):**

- **Scratch link:** the Scratch block you already know.
- **Type it:** short code to type in yourself. Typing beats copying and pasting, because your fingers learn the code.
- **Try it:** run it and see what happens.
- **Challenge:** a small change to make on your own.
- **Check:** a question to answer before moving on.

One lesson a week works well. If a lesson is easy, do two. If it's hard, repeat it. There's no rush.

**About accounts:** these lessons use only free tools that don't need an account. A parent or teacher can save the finished game in a repo on their own GitHub account (see Lesson 12).

## Scratch to Python cheat sheet

Keep this printed next to the computer. Everything you know in Scratch has a Python version.

| Scratch block | Python | What it does |
| --- | --- | --- |
| when green flag clicked | click the ▶ Run button | starts the program |
| say \[Hello!\] | `print("Hello!")` | shows text |
| set \[score\] to 0 | `score = 0` | makes a variable |
| change \[score\] by 1 | `score = score + 1` | adds to a variable |
| ask \[name?\] and wait | `name = input("Name? ")` | gets typing from the player |
| if … then | `if score > 10:` | does something only sometimes |
| if … then … else | `if …:` then `else:` | picks one of two paths |
| repeat 10 | `for i in range(10):` | repeats a set number of times |
| forever | `while True:` | repeats until the program stops |
| make a block (My Blocks) | `def launch():` | makes your own command |
| list | `targets = [1, 2, 3]` | holds many things |
| pick random 1 to 10 | `random.randint(1, 10)` | random number |
| touching \[sprite\]? | `rect.colliderect(other)` | checks if two things touch |
| x position / y position | `x` and `y` variables | where something is |

**Two big differences from Scratch:**

- **Spaces matter.** In Scratch, blocks snap inside other blocks. In Python, code goes "inside" an `if` or a loop when it is indented (pushed right with Tab). VS Code indents for you after a colon.
- **Y goes down.** In Scratch, y gets bigger as you go up. In pygame, y = 0 is the top of the window, and y gets bigger as you go down. This trips up everyone at first.

## Unit 1: Python basics (Lessons 1 to 4)

No graphics yet. These lessons teach the Python words you'll need for the game, using slingshot-themed mini programs.

### Lesson 1: Variables and print

**Scratch link:** "set", "change" and "say" blocks.

**Type it** (save as lesson1.py):

```python
name = "Blob"
power = 5
print("Get ready,", name)
print("Launch power:", power)
power = power + 3
print("Now power is", power)
```

**Try it:** click Run. Output shows in the Terminal panel at the bottom. For a Scratch-style variable monitor, click Run → Start Debugging and watch the Variables section on the left.

**Challenge:** add a `lives` variable that starts at 3, subtract 1, and print it.

**Check:** in Python, `=` doesn't mean "equals." What does it mean? (Answer: "put this value into this box.")

### Lesson 2: Asking questions and making choices

**Scratch link:** "ask and wait" plus "if then else."

**Type it:**

```python
power = int(input("Pick a launch power from 1 to 10: "))
if power > 7:
    print("WHOOSH! Way over the target!")
elif power < 4:
    print("Plop. It fell short.")
else:
    print("BOOM! Direct hit!")
```

**Try it:** run it several times with different numbers.

**Explain:** `input` always gives back text. `int(...)` turns the text into a number so Python can compare it. `elif` means "else if," which lets you check a second thing.

**Challenge:** add a message for exactly 10, such as "Into orbit!"

**Check:** what happens if you type "banana"? (It crashes. That's normal! Read the red error message together. Errors are clues, not failures.)

### Lesson 3: Loops and random numbers

**Scratch link:** "repeat until" and "pick random."

**Type it:** a guessing game where the target is a secret distance.

```python
import random

target = random.randint(1, 10)
tries = 0
guess = 0

while guess != target:
    guess = int(input("Guess the target distance (1-10): "))
    tries = tries + 1
    if guess < target:
        print("Too short!")
    elif guess > target:
        print("Too far!")

print("Hit in", tries, "tries!")
```

**Explain:** `!=` means "is not equal to." The loop keeps going while the guess is wrong, just like Scratch's "repeat until."

**Challenge:** give the player only 5 tries. If they run out, print "Out of ammo!" (Hint: change the `while` to also check `tries < 5`, using `and`.)

**Check:** which lines are inside the loop, and how can you tell? (They're indented.)

### Lesson 4: Functions (your own blocks) with turtle

**Scratch link:** "My Blocks" and the pen extension.

**Type it:** draw a tower of boxes, like the ones your character will knock over.

```python
import turtle

t = turtle.Turtle()
t.speed(0)

def box(x, y, size):
    t.penup()
    t.goto(x, y)
    t.pendown()
    for i in range(4):
        t.forward(size)
        t.left(90)

for level in range(3):
    box(0, level * 40, 40)

turtle.done()
```

**Explain:** `def box(x, y, size):` makes a new block called `box` with three inputs, exactly like a My Block with number inputs. Turtle's y goes up, just like Scratch.

**Challenge:** draw a second tower 100 steps to the right that is 5 boxes tall.

**Check:** why is a function better than copying the box code three times? (Fix it once and every box changes.)

## Unit 2: The game window and the launch (Lessons 5 to 8)

Now the real game starts. Each lesson adds to the same file, so save a copy at the end of each lesson (game5.py, game6.py and so on). If something breaks, you can go back.

### Lesson 5: Lists (planning your levels)

**Scratch link:** Scratch lists.

**Type it:** reuse your `box` function from Lesson 4, then replace the tower loop with this:

```python
towers = [3, 5, 2]

for i in range(len(towers)):
    for level in range(towers[i]):
        box(i * 80, level * 40, 40)
```

**Explain:** `towers` holds three numbers, one height per tower. `towers[0]` is the first item (Python counts from 0, not 1). `len(towers)` is how many items are in the list. A loop inside a loop draws every box in every tower.

**Challenge:** add a fourth tower by adding one number to the list. Notice that you didn't touch the drawing code at all.

**Check:** what is `towers[1]`? (5.) Later, each level of the game will be a list like this.

### Lesson 6: A pygame window and the game loop

**Scratch link:** "when green flag clicked" + "forever." Every game is one big forever loop that checks input, moves things, and redraws, about 60 times a second.

**Type it** (save as game6.py):

```python
import pygame

pygame.init()
screen = pygame.display.set_mode((800, 500))
clock = pygame.time.Clock()

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    screen.fill((135, 206, 235))
    pygame.draw.rect(screen, (90, 160, 60), (0, 450, 800, 50))
    pygame.draw.circle(screen, (220, 40, 40), (150, 350), 15)
    pygame.display.flip()
    clock.tick(60)

pygame.quit()
```

**Explain:**

- Colors are (red, green, blue), each from 0 to 255. (135, 206, 235) is sky blue.
- `fill` paints the background, then `rect` draws the ground and `circle` draws your character.
- `flip()` shows the finished picture. `clock.tick(60)` keeps it to 60 frames a second.
- The `QUIT` event means someone clicked the window's close button.

**Challenge:** change the sky to a sunset orange and make your character bigger. Add a brown rectangle for the slingshot post.

**Check:** where is (0, 0) in the window? (Top-left corner. Remember, y goes down.)

### Lesson 7: Dragging with the mouse

**Scratch link:** "when this sprite clicked" and "go to mouse-pointer."

**Type it:** start from game6.py and change it to this.

```python
import pygame

pygame.init()
screen = pygame.display.set_mode((800, 500))
clock = pygame.time.Clock()

start_x, start_y = 150, 350
x, y = start_x, start_y
dragging = False

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.MOUSEBUTTONDOWN:
            dragging = True
        if event.type == pygame.MOUSEBUTTONUP:
            dragging = False

    if dragging:
        x, y = pygame.mouse.get_pos()

    screen.fill((135, 206, 235))
    pygame.draw.rect(screen, (90, 160, 60), (0, 450, 800, 50))
    pygame.draw.line(screen, (100, 60, 20), (start_x, start_y), (x, y), 4)
    pygame.draw.circle(screen, (220, 40, 40), (x, y), 15)
    pygame.display.flip()
    clock.tick(60)

pygame.quit()
```

**Try it:** click and drag. The brown line is the slingshot band, stretching from the start point to your character.

**Explain:** `dragging` is a True/False variable, like a Scratch variable you set to 1 or 0. While the mouse button is down, the character follows the mouse.

**Challenge:** when you let go, make the character snap back to the start point. (Hint: set `x` and `y` inside the `MOUSEBUTTONUP` part.)

**Check:** why do we draw the line before the circle? (Things drawn later go on top, like Scratch layers.)

### Lesson 8: Launch!

**Scratch link:** your Scratch game probably used speed variables. Python uses the same idea: **velocity** is how far something moves each frame, split into sideways (`vx`) and up/down (`vy`).

**Type it:** add two new lines under `dragging = False`:

```python
vx, vy = 0, 0
flying = False
```

Replace the two mouse checks in the event loop with these, and add the R key to reset:

```python
        if event.type == pygame.MOUSEBUTTONDOWN and not flying:
            dragging = True
        if event.type == pygame.MOUSEBUTTONUP and dragging:
            dragging = False
            flying = True
            vx = (start_x - x) * 0.15
            vy = (start_y - y) * 0.15
        if event.type == pygame.KEYDOWN and event.key == pygame.K_r:
            x, y = start_x, start_y
            flying = False
```

Then add movement right after the `if dragging:` part:

```python
    if flying:
        x = x + vx
        y = y + vy
```

**Try it:** pull back and to the left, then let go. Press R to reset.

**Explain:** the launch speed is the distance from where you let go back to the start point. Pull farther and it goes faster. Pull down-left and it flies up-right, the opposite way, just like a real slingshot. The 0.15 is the "band strength."

**Notice the problem:** it flies in a straight line forever, right off the screen. Real things fall. That's next lesson.

**Challenge:** try band strengths of 0.05 and 0.3. Which feels best?

**Check:** if you let go exactly at the start point, what happens? (Speed is 0, so it doesn't move.)

**Optional art break:** if you want your own drawings in the game now, jump to "Your own character art" in Lesson 12 and do that step. Everything else still works the same. You can also leave the circle and boxes for later. Do whichever feels more fun.

## Unit 3: Physics, targets, levels and sharing (Lessons 9 to 12)

### Lesson 9: Gravity and bouncing

**Scratch link:** if your Scratch game had "change y speed by -1" in a forever loop, that's gravity. Same idea here.

**Type it:** add these two lines near the top, under `flying = False`:

```python
GRAVITY = 0.4
GROUND = 435
```

Then replace your `if flying:` part with this:

```python
    if flying:
        vy = vy + GRAVITY
        x = x + vx
        y = y + vy
        if y > GROUND:
            y = GROUND
            vy = -vy * 0.5
            vx = vx * 0.8
```

**Try it:** launch at different angles. You should see a curved arc, then a few bounces.

**Explain:**

- Gravity doesn't move the character directly. It changes the **speed**: every frame, falling gets a little faster. That's what makes the curve.
- GROUND is 435 because the grass starts at 450 and the character's radius is 15.
- On a bounce, `vy` flips direction and keeps only half its strength (`* 0.5`). Friction slows `vx` (`* 0.8`).
- Names in ALL CAPS are a Python habit for settings that don't change.

**Challenge:** make a "moon mode" with gravity 0.1. Then try a super-bouncy ball with 0.9 instead of 0.5.

**Check:** what would happen with GRAVITY = -0.4? Guess first, then try it.

### Lesson 10: Targets and collisions

**Scratch link:** "touching \[sprite\]?" and "hide."

**Type it:** under the GROUND line, make a list of boxes. `pygame.Rect(x, y, width, height)` is a rectangle Python can test for touching.

```python
targets = [
    pygame.Rect(600, 410, 40, 40),
    pygame.Rect(600, 370, 40, 40),
    pygame.Rect(680, 410, 40, 40),
]
```

After the `if flying:` part, check for hits:

```python
    me = pygame.Rect(x - 15, y - 15, 30, 30)
    for box in targets[:]:
        if me.colliderect(box):
            targets.remove(box)
```

In the drawing part, after the ground, draw the boxes:

```python
    for box in targets:
        pygame.draw.rect(screen, (160, 110, 60), box)
```

**Explain:** `me` is an invisible square around your character. `colliderect` asks "are these two rectangles touching?" `targets[:]` loops over a copy of the list, so removing a box while looping is safe.

**Challenge:** add a fourth box on top of the stack. Then make your own tower shape.

**Notice:** when you knock out the bottom box, the top one floats in the air. Real toppling needs a physics engine. See "Where to go next" in Lesson 12.

**Check:** why is `me` 30 wide? (The circle's radius is 15, so it's 30 across.)

### Lesson 11: Score and levels

**Scratch link:** lists, "broadcast next level," and a score variable shown on screen.

**Type it:** replace your `targets = [...]` list with a list of levels. Each level is a list of box positions.

```python
levels = [
    [(600, 410), (600, 370)],
    [(550, 410), (650, 410), (650, 370), (650, 330)],
    [(500, 410), (600, 410), (700, 410), (600, 370), (600, 330)],
]
level = 0
score = 0

def load_level(n):
    boxes = []
    for (bx, by) in levels[n]:
        boxes.append(pygame.Rect(bx, by, 40, 40))
    return boxes

targets = load_level(level)
font = pygame.font.SysFont(None, 36)
```

In the hit check, add points: put `score = score + 100` under `targets.remove(box)`.

After the hit check, move on when every box is gone:

```python
    if len(targets) == 0 and level < len(levels) - 1:
        level = level + 1
        targets = load_level(level)
        x, y = start_x, start_y
        flying = False
```

At the end of the drawing part, just before `flip()`, show the score:

```python
    text = font.render("Level " + str(level + 1) + "   Score " + str(score), True, (0, 0, 0))
    screen.blit(text, (20, 20))
```

**Explain:** the game code never changes when you add a level. You just add another list of positions. That's the big idea from Lesson 5. `str(...)` turns a number into text so it can be joined with words.

**Challenge:** add a `shots` counter that starts at 3 and goes down by 1 each launch. Show it on screen. When it reaches 0, show "Try again!" (Hint: subtract inside the `MOUSEBUTTONUP` part.)

**Check:** what happens after the last level? Can you show "You win!" there?

### Lesson 12: Make it yours and share it

**Your own character art (optional):** you can draw anything you like in Scratch's costume editor and use it in Python. Scratch draws in vector mode by default, which Python can't load reliably, so first click **Convert to Bitmap** at the bottom left of the editor. Then right-click the costume and choose **export**. It saves as a PNG in your slingshot folder. Then in Python:

```python
hero = pygame.image.load("hero.png")
hero = pygame.transform.scale(hero, (40, 40))
```

Replace the `pygame.draw.circle` line with `screen.blit(hero, (x - 20, y - 20))`.

**Using any other picture:** the same two lines work for any image, wherever it came from.

- **Where pictures can come from:** your Scratch drawings, a drawing app (Paint, Krita and Piskel are free), a photo you took, or a picture you found online. For anything from the internet, check that it's free to use, and note where it came from.
- **Use PNG or JPG files.** PNG is best for characters because it can have a see-through background. A JPG always has a solid rectangle behind the picture. SVG files won't load. In a drawing app, choose **Export as PNG**.
- **Put the file in your slingshot folder**, next to your game file, and spell the name exactly. `hero.png` and `Hero.png` can be different names to Python.
- **If the picture looks too big or too small**, change the numbers in `pygame.transform.scale(hero, (40, 40))`. They're width and height in pixels.
- **If the corners show a white box**, the picture doesn't have a see-through background. Use a PNG, and add `.convert_alpha()` to the end of the load line: `pygame.image.load("hero.png").convert_alpha()`.
- **If you get "No file named…"**, the file isn't in the same folder as your game, or the name is spelled differently.
- **Pictures for other things:** the same idea works for the pigs, the boxes, the slingshot and the background. Load each picture once at the top of the file, then draw it each frame with `screen.blit`.

Any of these is fine. Use shapes, your drawings, or a mix.

**Polish ideas (pick two or three):**

- A background image you drew in Scratch, exported the same way.
- Different box colors for each level.
- A dotted trail showing where the last shot went. (Hint: keep a list of past positions and draw small circles.)
- A title screen that says "Click to start."

**Write a README:** in VS Code, make a new file called README.txt. Write the game's name, how to play, and what you learned. Real programmers write one for every project.

**Share it:** demo it for the family. A parent can upload the folder to a repository on the parent's GitHub account, so the project is saved and can be shown off later.

**Where to go next:**

- **pymunk** is a free physics library that works with pygame. It makes towers actually topple, with mass and friction. It's a great "version 2" project.
- Revisit your Scratch game and compare it with the Python one. What was easier in each?
