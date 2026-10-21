# CS-350 Emerging Systems Architectures and Technologies

Portfolio artifacts from my CS-350 course at SNHU, built on a Raspberry Pi 4B running Ubuntu Server 24.04 with Python.

## Artifacts

| Folder | What it is |
|---|---|
| `Final Project - Smart Thermostat/` | `Thermostat.py`, the state machine diagram (PDF), and the hardware architecture report (DOCX) |
| `Milestone Three - Morse Code/` | `Milestone3.py` and its state machine diagram (PDF) |

## Reflection

**Summarize the project and what problem it was solving.**
The final project was a low-level thermostat prototype for a company that wanted to move into the smart thermostat market. The Pi reads the room temperature from an AHT20 sensor over I2C and runs a three-state machine (off, heat, cool). It drives a red and a blue LED to show whether it's heating or cooling, takes input from three buttons to change the mode and the set point, shows the date, time, temperature, and set point on a 16x2 LCD, and sends a status line to a simulated server over UART every 30 seconds. The second artifact is the Milestone Three Morse code project. It blinks messages in Morse on two LEDs, shows the message on the LCD, and switches messages with a button press. I picked these two because together they cover pretty much everything the course was about: GPIO, I2C, UART, interrupts, threading, and state machines.

**What did you do particularly well?**
I think the state machine design is the strongest part. Each state handles its own LEDs on entry and exit, so the light behavior always matches the state and I never had to chase stray LEDs. I'm also happy with the debugging. When my red button didn't respond, I used the multi-button test to show that the other two worked, which pointed straight to the wiring instead of the code. The jumper turned out to be one row off on the breadboard.

**Where could you improve?**
Hardware setup took me longer than it should have, especially the LCD wiring, and I'd be more careful matching the lab guide photos the first time. On the software side, the set point has no upper or lower limits, and the temperature thresholds could use a small buffer so the LEDs don't flicker between pulsing and solid when the reading sits right at the set point.

**What tools and/or resources are you adding to your support network?**
The Raspberry Pi and Adafruit documentation, the gpiozero and python-statemachine docs, datasheets for parts like the AHT20, and the Raspberry Pi community forums. Remote work over SSH and SCP also became part of my normal workflow.

**What skills from this project will be particularly transferable to other projects and/or course work?**
Modeling a system as a state machine before coding it is something I'll use well beyond embedded work, in game logic, UI flows, and backend workflows. Event-driven programming with interrupts, running work on background threads, and talking to hardware over standard protocols like I2C and UART all carry over to any IoT or systems role. Breaking a hardware problem down to test one piece at a time is just good debugging in general.

**How did you make this project maintainable, readable, and adaptable?**
I kept the code split into clear pieces: the state machine class, a separate display manager class for the LCD, and small handler methods for each button. Every pin number is defined once at the top, so moving a component to a different GPIO pin is a one-line change. I used descriptive names and short comments, and the serial output is built in one method, so changing the server format only touches one place. The state machine diagram documents the behavior, so someone new can see how it works before reading any code.
