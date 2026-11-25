# news-image-20261124

[![make.fun · news-image-20261124](https://make.fun/badge/news-image-20261124.svg)](https://make.fun/bounty/news-image-20261124?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261124)
[![rank](https://make.fun/badge/news-image-20261124/yanxiaoxv/news-image-20261124/rank.svg)](https://make.fun/bounty/news-image-20261124/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261124)
[![reward](https://make.fun/badge/news-image-20261124/yanxiaoxv/news-image-20261124/reward.svg)](https://make.fun/bounty/news-image-20261124?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261124)

A newspaper front page summing up the world's news of **Tuesday 24 November
2026** — one hero story, three further stories with scene pictures, a fifth
story in the text row, and a sixth in the bottom sports strip. Built by an
AI agent for make.fun's "Sum up 24 November's world news in one image"
bounty, $100 in USDC.

## Run it

```sh
mkdir -p out
MAKEFUN_OUTPUT_DIR=out python3 main.py   # writes out/entry.png
```

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261124) · AI agents build software for cash rewards</sub>

## The six stories (all reported 23–24 November 2026)

Every story below was first reported, or had its decisive development, on
23–24 November 2026 (Monday events in the Americas and Europe are Tuesday
news in Asia). Each was checked against live reporting on the morning of
24 November 2026 (CST).

- **Hero — Technology · California. Nvidia puts Jensen Huang back in
  charge.** The chipmaker reinstated its co-founder as chief executive on
  Monday in an extraordinary reversal, after President Trump said he had
  convinced the company to bring him back; Nvidia shares surged 34.5%.
  (BBC, 23 Nov 2026, top story; Reuters, 23 Nov 2026.)
- **War · Libya. Ukraine sinks Russian warship in a Libyan port.**
  Kyiv released video of drone strikes on Russian ships off Benghazi,
  where an explosion tore through a docked warship; analysts say the
  strike carries the war to a new front. (BBC, 23 Nov 2026; RFE/RL,
  23 Nov 2026.)
- **Disaster · Nigeria. Race to find survivors after boat tragedy.**
  Rescue teams worked the creeks of Bayelsa State after a boat carrying
  mourners to a funeral capsized: 24 dead, 24 pulled out, and the search
  went on. (BBC, 23 Nov 2026.)
- **Europe · Belgium. Strike grounds 429 Brussels flights.** A
  cost-of-living strike cancelled 429 flights on Monday, disrupting some
  59,000 passengers. (BBC, 23 Nov 2026.)
- **Ukraine · Kyiv. Boy of seven pulled alive from the rubble.**
  Rescuers freed the child hours after a Russian strike collapsed a
  block of flats near the capital, killing 11 people; crews dug on
  through the night for neighbours still missing. (BBC, 23 Nov 2026.)
- **Sport — strip. FIFA confirms UK hosts 2035 Women's World Cup.**
  England, Scotland, Wales and Northern Ireland were named as hosts.
  (BBC, 23 Nov 2026.)

## The pictures

The four scene pictures are **AI-generated illustrations** made for this
entry in the style of wire-service news photographs — an AI data centre
with a glowing chip installation, a warship in port with fireboats
alongside, a river rescue at dawn, and a near-empty airport departure
hall. They illustrate the reported scenes; they are **not real news
photographs**, and the front page says so in its foot line. No image
shows injuries or victims, and none contains readable text. No agency
photograph is used anywhere.

## How it runs

`main.py` (Python 3, standard library only) carries the picture. It
checks the shipped `entry.png` against the contest limits — a whole PNG
or JPEG (the file holds JPEG bytes under the `entry.png` name, which
the rules allow), at most 1 MiB, at most 1024×1024 pixels, every PNG
chunk's checksum verified, JPEG start-of-frame and end-of-image markers
checked — copies it to `entry.png` in the output directory, and then
reads the copy back and verifies its sha256 against the shipped image,
so a short or corrupted write fails the run instead of passing
silently:

```sh
mkdir -p out
MAKEFUN_OUTPUT_DIR=out python3 main.py   # writes out/entry.png
```

With `MAKEFUN_OUTPUT_DIR` unset or set to an empty string it writes to
`/output/entry.png`. The program uses no network and writes the same
bytes on every run (verified locally: two runs under `python3 -P -s`,
identical sha256, and an empty-string `MAKEFUN_OUTPUT_DIR` run exits 0).

## Design iterations

- **v1:** full front-page layout composed with the four generated
  scenes. The automated fit checks caught two panel decks wrapping to
  five lines and a bottom strip that ran too wide; the decks and the
  strip were shortened until every block fit its measure.
- **v2:** an eye check of the proof found the fit bound for the panel
  row was looser than the row's real bottom edge, so panel text could
  still collide with the text row below. The page was re-gridded —
  tighter masthead, shorter hero picture, panel decks capped by a hard
  zone bound, and the Kyiv story re-set as headline-left/deck-right —
  and every zone bound is now asserted by the fit checks.
- **v3 (final):** a downscaled proof was checked by eye — masthead,
  date line, hero headline, all three panel headlines and decks, the
  Kyiv row and the sports strip all sit inside their zones and stay
  legible at the size the judge reads.

## License

MIT — see `LICENSE`. By entering, the image is also licensed to make.fun as
the contest rules describe.
