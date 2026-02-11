---
layout: default
title: Queer Coded Fortune Teller
---

[Home](/) | [Blog](/blog) | [Projects](/projects) | [Resume](/resume)

# Queer Coded Fortune Teller

The first iteration of the Queer Coded Fortune Teller (QCFT) project explores randomness and fortune telling, while serving as a practical refresher in rapid prototyping and Python development. The project has three core tasks:

1. Load tarot card images and meanings, then pick three cards at random.
2. Provide a Tkinter GUI where a user can:
   - generate a three-card tarot spread,
   - redraw a spread,
   - print the generated fortune via button actions.
3. Print the generated fortune on a thermal printer.

![RPi Screen](/pictures/RPi_screen.png)

### Hardware

This iteration keeps the hardware intentionally minimal to get the end-to-end system working:

- **Raspberry Pi Zero 2 W (RPiZ2W)**
- **QR204-N32-2012 thermal printer**

### Software

Given the Raspberry Pi Zero 2 W’s limited resources, the software takes a deliberately lightweight approach built around Python and Tkinter:

- **tkinter**: the GUI framework, driven by Tkinter’s event loop (`root.mainloop()`)
- **python-escpos**: thermal printer control via ESC/POS commands
- **PIL (Pillow)**: image loading, resizing, dithering, and composition for print output
- **os, json, random**: filesystem traversal, meaning lookup, and random selection

Card images are stored as `.png` files, while upright and reversed meanings are stored in a `.json` file. The application selects three cards randomly and independently assigns each one an upright or reversed orientation.

### UI flow and execution model

At startup, the application loads and preprocesses card assets, initializes the serial printer interface, and then hands control over to the Tkinter event loop.

The QCFT application follows an event-driven execution model: after initialization, control lives inside Tkinter’s main event loop. User actions (button clicks) trigger callback functions, which update the UI and invoke printer actions.

Conceptually, the GUI behaves like a small state machine, with user events driving transitions between states such as:

- **Idle / Displaying Spread**: three cards are shown with meanings
- **Printing**: print job is in progress and the UI must avoid conflicting actions

In the GUI, three cards are displayed side-by-side with their meanings below using a `grid` layout for consistent alignment. Two buttons control the main transitions:

- **Draw Again**: triggers a new random draw, updates images and text in-place.
- **Print Fortune**: composes the three card images into a single print image and sends it to the printer over the serial port.

To prevent print artifacts, such as shifted segments caused by overwhelming the printer buffer, the print pipeline includes brief pacing delays between data transfers.

At this stage, printing is implemented as a blocking operation: while the printer is printing, the Tkinter GUI remains unresponsive until the job completes. This is acceptable for a first iteration and also highlights an obvious next improvement: moving long-running I/O off the UI thread (e.g., via `after()` scheduling or a worker thread + queue) to keep the interface responsive during printing.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/J1-NpNGoC5g" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> The operation of QCFT
