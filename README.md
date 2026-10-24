# password-strength-visualizer

A single web page that scores a password as you type: a live strength meter, an
entropy estimate in bits, an estimated offline crack time, and a checklist of
rules it passes. Everything runs in the browser and nothing you type is ever
sent anywhere.

**Live:** https://siddique-12300983.github.io/password-strength-visualizer/

## What it does

- Live meter that moves from "very weak" to "very strong" as you type
- Entropy in bits, based on the character set used and the length
- Estimated time to crack offline, assuming a fast attacker at about 100 billion
  guesses per second
- A rules checklist (length, character variety, and whether the password is an
  obvious pattern)
- A show/hide toggle

Obvious passwords (common words, `123456`, repeated or sequential characters)
are capped low, because their real guessability is far lower than the raw
length-times-charset maths would suggest.

## Private by design

There are no network requests in the page at all: no analytics, no fonts, no
APIs. The password is scored with JavaScript on your device. You can read the
page source and confirm there is nothing sending it anywhere. That is the whole
point of doing this client-side.

## How the estimate works

Entropy is `length x log2(charset size)`, where the charset size grows with the
kinds of characters used (lowercase, uppercase, digits, symbols). The crack-time
estimate takes half of the `2^entropy` search space and divides by the guess
rate. It is a guide, not a guarantee: a real attacker uses dictionaries and
rules, which is why this page also penalises obvious passwords rather than
trusting the maths alone.

## Running it locally

It is one file with no build step. Open `index.html` in a browser, or serve the
folder:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Tech

Plain HTML, CSS and JavaScript. No libraries, no build tools. Dark theme,
works on mobile.

## License

MIT. See [LICENSE](LICENSE).
