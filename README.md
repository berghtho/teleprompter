# Teleprompter

A teleprompter for giving talks, in a single HTML file. It scrolls your script at a set speed in words per minute, keeps the lines you're reading in a highlighted band, and shows slide by slide whether you're ahead of or behind your plan.

No install, no build, no server. Everything stays on your machine: the page loads nothing from the network.

## Quick start

1. Download [`teleprompter.html`](teleprompter.html) (on GitHub: open it and click *Download raw file*), or clone this repo.
2. Open it in your browser. Double-clicking the file is enough.
3. Press <kbd>E</kbd>, paste your script, and click **Save and close**.
4. Press <kbd>Space</kbd> to start scrolling. Adjust the speed with <kbd>↑</kbd> and <kbd>↓</kbd>.

## Writing the script

One block per slide: a line with the slide number and title, a blank line, then the text.

```text
1  Welcome

Good morning, everyone.
Today is about *one* idea.

A blank line starts a new paragraph.

2  The problem

Every slide starts with its number and title on a line of its own.
```

- **Blank line**: new paragraph.
- **Single line break**: new line on screen. Use it to mark a pause.
- `*word*`: emphasis, shown bold and yellow.
- The slide number is a label for the slide list and the top bar. It doesn't have to match your deck.

A paragraph that is a single line starting with a number, like `3 reasons to care`, is read as a new slide. Write the number as a word, or break the paragraph over two lines.

## Controls

| Key | Action |
| --- | --- |
| <kbd>Space</kbd> | Play / pause |
| <kbd>↑</kbd> <kbd>↓</kbd> | Faster / slower, in steps of 10 wpm (90–200 wpm, default 120) |
| <kbd>→</kbd> | Next slide |
| <kbd>←</kbd> | Start of the current slide; press again for the previous one |
| <kbd>+</kbd> <kbd>-</kbd> | Text size |
| <kbd>[</kbd> <kbd>]</kbd> | Move the reading band up / down |
| <kbd>S</kbd> | Slide list |
| <kbd>E</kbd> | Edit the script (<kbd>Esc</kbd> closes the editor without saving) |
| <kbd>M</kbd> | Mirror the text, for teleprompter glass |
| <kbd>T</kbd> | Reset the clock |
| <kbd>H</kbd> | Hide / show the shortcut help |
| <kbd>Home</kbd> | Back to the top |

The buttons at the bottom of the screen (previous, slower, play, faster, next) work with a mouse or a touch screen. You can also scroll by hand at any time, even while it's playing.

## The top bar

- **Clock**: talk time since you first pressed Play. It keeps counting through pauses, so it shows your real talk time. <kbd>T</kbd> resets it.
- **Current slide**: its title, its position (for example `5/34`), when it's planned to start at the current speed, and how far off you are: grey within 45 seconds, red when you're late, green when you're early.
- **wpm · ~min**: the current speed and the estimated length of the whole talk (words ÷ wpm, plus 3 seconds per slide for the gap between slides).
- **size** and **band**: text size and reading band position.
- **media keys**: see [Presenting with PowerPoint](#presenting-with-powerpoint).

## Saving your script

The editor (<kbd>E</kbd>) has these buttons:

- **Save and close** keeps the text in this browser's local storage. Speed, text size and band position are remembered there too, so reopening the file brings everything back.
- **Download as .txt** and **Load .txt…** move the script out and in as a plain text file. After loading, click **Save and close**.
- **Save as .html (text embedded)** downloads a copy of the prompter with your script built in: one file for this talk that you can take to another machine.
- **Restore built-in script** puts the file's built-in script back into the editor. In this blank template, that's empty.

Text saved in the browser takes precedence over the built-in script. Every copy of the prompter uses the same storage key (`teleprompter-script`), and browsers can share storage between local files. If you keep one prompter file per talk, give each its own key (search for `const KEY=` in the file) so their saved texts don't mix.

## Presenting with PowerPoint

To control the prompter while PowerPoint (or any other app) has the focus, click **media keys: off** in the top bar to switch them on. Your keyboard's media keys then drive the prompter: play/pause starts and stops scrolling, next/previous track jump between slides, and seek forward/back (if your device has them) change the speed.

This uses the browser's Media Session API: the page loops a silent audio clip so the browser sends the media keys to it. Leave it off if Teams or a YouTube tab keeps grabbing them.
