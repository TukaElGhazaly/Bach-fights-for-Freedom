# Bach's Cell: ordnungd[1717]

A daemon of ducal routine traps the music in one bar and keeps only the last visitor inside.

## Author and course

- **Author:** [Name Surname]
- **Studio:** Pandaemonium: Daemons for Weimar
- **Course:** M.Sc. Digital Technologies in Architecture and Design (DTAD), WiSe 2026/27
- **Chair:** Informatics in Architecture and Urbanism (InfAU), Faculty of Architecture and Urbanism, Bauhaus-Universität Weimar
- **Teaching staff:** Reinhard König, Martin Bielik, Egor Gaydukov, Egor Gavrilov, Jan Willmann, Michael Braun, Thomas Pearce
- **Exercise:** Nonsense Project, 15.10. to 29.10.2026
- **Submission date:** [DD.MM.2026]

## Links

- **Live demo:** https://tukaelghazaly.github.io/Bach-fights-for-Freedom/Bach%27s%20Cell.html
- **Source repo:** https://github.com/TukaElGhazaly/Bach-fights-for-Freedom
- **Miro frame:** https://miro.com/app/board/uXjVHn1RS88=/?moveToWidget=3458764689890548590
- **60-second showreel:** on the Miro frame

## The task

The Nonsense Project is the two-week, individual start of the studio. I drew one theme, a strange situation in a city where things have spirits, and one constraint, a limit on the daemon I imagined for it. With a coding agent I built a prototype that shows what my daemon would do. Sensors and AI services could be faked, as long as the result was specific and believable. A daemon is not a script, so even a fake one had to decide for itself.

## Theme and constraint

- **Theme 9:** Everyone remembers certain places in the city differently.
- **Constraint 4:** The daemon remembers only its last visitor.

## The daemon

### Concept

In November 1717 Duke Wilhelm Ernst locked his court musician, Johann Sebastian Bach, in a room in Weimar for asking to leave. This project imagines that the room never let go. The duke's strict court routine lives on as a spirit in a narrowing passage that ends in a small cell. While the passage is empty, a Bach piece plays freely. When someone walks deeper in, the music gets stuck on the bar that was playing and repeats it, the colour drains, and the sound slowly sinks and decays. The spirit asks every visitor's name. The last one inside cannot leave until someone new arrives. Because it remembers only its last visitor, every person leaves the place carrying a different bar, and that one bar keeps returning after they are gone. Nobody hears the same room twice.

### Perceive, think, act

- **It perceives:** who stands at the wide mouth of the passage, who has crossed into the narrow throat, how deep they are, how long they stay, and the name each visitor gives. It cannot see faces, hear voices or know anyone it has already forgotten.
- **It thinks:** it wants order and keeping: the music held in one bar, someone always inside. Each time the loop comes round it decides how strict to be, from how many people are inside, how long they have stayed and whether the last one is trying to leave.
- **It acts:** it freezes the music on one bar, drains the colour, distorts the sound and lowers its pitch up to an octave, decides how far the exit door opens, and screams the name of the last visitor if they try to escape. After they leave, it plays their bar again.
- **Real or faked:** the music, the looping, the distortion, the spoken names and the daemon's decisions really run in the browser. The visitors are simulated (or controlled by hand), and there are no real sensors in a real passage.

### One visitor

[Draft, edit freely.] Lena, a second-year architecture student, cuts through the passage at night on her way home from the studio, a jury tomorrow. At the mouth she hears the Prelude in C, light and running. The daemon stops her: *who are you?* She types "Lena" and steps further in. On bar 7 the music catches, and that bar comes round again, and again, a little slower and a little lower each time. The drawing turns grey. She walks on, looking for the way out, but the door at the end only opens a crack. When she turns back toward the street, the room says her name, loudly, and the bar warps further. She is the last one inside, so she waits. A simulated stranger wanders in behind her; the door gives, and she leaves. The music frees itself, but a minute later bar 7 returns, hers, played for nobody. She feels oddly kept, then oddly replaced. She takes away one bar of Bach she cannot stop humming, and the knowledge that the next person will remember the passage by a different one.

## How to use it

1. Open the live demo. You see a title page with three chapters: the history of Bach and the duke, the simulation, and the game.
2. Open the simulation and press **Wake the daemon (sound on)**. The plan and section of the passage appear, the piece plays freely, and simulated visitors start to arrive on their own.
3. Switch to **Control the people**, give a name when the daemon asks, and drag your person from the mouth into the throat. The music locks onto the current bar; watch the daemon log, its state panel and the one memory it keeps.
4. Try to bring the last visitor back out, or wait for someone new to enter. Change the Bach piece to hear how a different bar gets trapped.
5. For the game, choose **Play the game**, give your name and enter the passage. **W A S D** to walk, **Shift** to run, **Space** to shove, **E** to break free at the grate, **M** mute, **R** restart. On a phone, use the on-screen controls.
6. Tips: wear headphones, since the browser speaks your name. Stay in the loop a long time to hear the pitch sink a full octave. Host a race and share the QR code so friends can join from their own phones.

## Technical implementation

- **Frontend:** a single HTML file, vanilla JavaScript, SVG/CSS drawings and Canvas 2D for the game; Web Audio API for the synthesised piano and distortion, Web Speech API for the spoken names.
- **Hosting:** GitHub Pages, because the project is one static HTML file and needs no server
- **Data sources and APIs:** none at runtime. Multiplayer races use the hosting page's shared room (`window.claude.use('room')`) when available; without it the game runs single-player.
- **Models while it runs:** none. The daemon's decisions are rule-based.
- **Notable libraries:** qrcode-generator 1.4.4 (from cdnjs) for the race QR code.
- **Run locally:**

```sh
git clone https://github.com/TukaElGhazaly/Bach-fights-for-Freedom.git
cd Bach-fights-for-Freedom
npm install
npm run dev
# opens http://localhost:8000/Bach%27s%20Cell.html
# (or simply open "Bach's Cell.html" in a browser)
```

## Working with AI

- **Coding agents used:** Claude Code, model Claude Opus 5.5 (`claude-opus-5-5`)
- **Key prompts** (two to five that really moved the project):
  1. "The 2D simulation is nice and perfect. However, I want a home screen with bars: history and context about Bach and the duke, the simulation, and a bar for a game."
  2. "Make the demons steal the music sheet to add more challenge. Also make the home screen have floating notes, but they get distorted and change colours."
  3. "When the user is about to escape, make the demons pull the users harder, and the users have to press E multiple times to escape. Try to make it multiplayer with a QR code."

**Reflection** (150 words at most): What unlocked progress was settling the 2D simulation first: once the daemon's rules worked in the plan and section drawings, the agent could reuse the same daemon for the home screen and the game. Short, concrete prompts about one mechanic at a time (stolen pages, pressing E to break free) worked better than broad requests. The agent went sideways when a feature depended on where the page was hosted: multiplayer only works through Claude's shared room, so on a plain static host the race falls back to single-player. Repeatedly asking for a fresh link to test each change also slowed things down. Next time I would decide the hosting first, keep the project in Git from day one instead of one large uploaded file, and write the daemon's rules down as a short spec before asking for the game layer on top of them.

## Credits, assets, licenses

- **Fonts:** IM Fell English, JetBrains Mono, Schibsted Grotesk, via Google Fonts, SIL Open Font License 1.1
- **Data:** historical frame (Bach held in the Weimar *Landrichterstube*, 6 Nov to 2 Dec 1717) from Christoph Wolff, *Johann Sebastian Bach: The Learned Musician* (W. W. Norton, 2000), and the Bach-Archiv Leipzig; the link to the *Well-Tempered Clavier* is a legend (Ernst Ludwig Gerber, 1790), not a documented fact
- **Images and sounds:** music by J. S. Bach (public domain): Prelude in C major BWV 846, Cello Suite No. 1 Prelude BWV 1007, Minuet in G BWV Anh. 114 (now usually credited to Christian Petzold), Jesu, Joy of Man's Desiring BWV 147, Toccata in D minor BWV 565. Simplified arrangements, synthesised in the browser. All drawings are generated in code. All visitors and characters are invented.
- **Third-party code:** qrcode-generator by Kazuhiko Arase, MIT License
- **This repo:** code under the MIT License; texts and drawings under CC BY 4.0

The daemon is the spirit of the court's routine, not a portrait of the duke.
