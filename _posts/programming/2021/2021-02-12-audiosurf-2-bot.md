---
title: Audiosurf 2 Bot
date: 2021-02-12
categories: programming
---

I finally got a simple [Audiosurf 2 Bot](https://github.com/kennguyen01/audiosurf-bot) up and running. I had the thought of building this bot for a long time but never made the commitment to just sit down and do it. Here's what it looks like:

<div align="center">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/aErTi7NPSMo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

This was the first working prototype. There were still glaring issues about accuracy and performance. I fixed some minor problems like the ship not hitting far left or far right blocks. It gets the job done but it's still a crappy bot. There are still a few issues I have not been able to address yet.

<!--more-->

## Maxing Out My CPU

The first issue is that running real time detection requires a lot of processing powers. Since I'm using `pywin32` for capturing game screenshots, I can get at least 30fps when I reduce the capture region to be 600x500. Those images are sent to the cascade classifiers for detection. Blocks and spikes have their own separate classifier. This process eats up a lot of CPU. My PC fans are spinning like crazy when I run the bot while playing the game.

This is an issue specific to creating detection bot for a rhythm game like Audiosurf 2. The game can have many objects on the screen at once. Using computer vision to detect everything is inherently expensive. If my bot is reading from the game memory directly, it does not need that much processing. A minor performance fix I did was increasing the minimum size of the object to avoid detecting far away objects:

```py
block_cascade.detectMultiscale(image=screenshot, minSize=(40, 40))
```

## Keyboard Only

The second issue is the game's countermeasure for scripting. Audiosurf 2 can be played with the mouse, keyboard, or controller. It only accepts virtual inputs from the keyboard. It blocks mouse movements from my Python script. I tried different libraries such as `mouse`, `pyautogui`, `pydirectinput`, and `pynput`. The movements from these libaries are only registered when the game is paused or not running. It did not matter whether I knew the exact coordinates of the objects on screen, I cannot move the mouse cursor there.

Moving the ship with the keyboard is clunky. To move left or right, I need to send a virtual input to hold that key. Moving in the opposite direction means I need to release the previous key and hold the other key.

```py
# Virtual key hex codes
a = 0x41
d = 0x44

def hold_left():
    win32api.keybd_event(a, 0, 0, 0)

def hold_right():
    win32api.keybd_event(d, 0, 0, 0)

def release(self):
    win32api.keybd_event(a, 0, win32con.KEYEVENTF_KEYUP, 0)
    win32api.keybd_event(d, 0, win32con.KEYEVENTF_KEYUP, 0)
```

I chose to hold down the key because it looks smoother on screen. If the key is just pressed, the ship starts to have seizures when there are a lot of blocks and spikes coming. I have not tried using a lower level language like C++ to send mouse inputs directly to driver level so I might get around to it in the future.

## Insufficient Training

The last issue is accuracy of detection. This is due to the small size of my training data:

- Positive samples:
  - Blocks: 1000+
  - Spikes: 500+
- Negative samples:
  - Blocks: 350
  - Spikes: 300

To get better classifiers, I probably need thousands more positive and negative samples. I spent the most time preparing the data and training the classifiers. It taught me the importance of preparing good data for training but I rather not going through the long and tedious process again.