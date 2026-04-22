# Mifflin Bingo

This is a small static bingo card web app built for sharing rotating bingo card images through a single QR code.

When someone opens the main page with no query parameters, they see the admin screen. That screen shows one QR code to print or display during the event.

When a person scans the QR code:

1. The app increments a scan counter stored in `localStorage`.
2. It assigns the next bingo card in the rotation.
3. It redirects the user to a simple card screen that shows the bingo card image.
4. The user can download that image from the same screen.

## How It Works

- The main app lives in `index.html`.
- Styling lives in `bingo-style.css`.
- The bingo card images live in `img/`.
- The QR code points to `?scan=1`.
- Each scan rotates through the five card images in order:
  `card1.png` -> `card2.png` -> `card3.png` -> `card4.png` -> `card5.png` -> repeat

The scan counter is browser-local, which means it works well for a simple single-device setup. If you host the admin page on multiple devices, they will not share the same counter unless you replace `localStorage` with a shared backend.

## Files

- `index.html`: admin screen, QR generation, scan routing, and user card screen
- `bingo-style.css`: all visual styling
- `img/card1.png` through `img/card5.png`: the bingo card images shown to users

## Customizing Cards

If you want to change the bingo cards, replace the files in `img/` or update the `CARD_IMAGES` array in `index.html`.

Current image list:

```js
const CARD_IMAGES = [
  "./img/card1.png",
  "./img/card2.png",
  "./img/card3.png",
  "./img/card4.png",
  "./img/card5.png",
];
```

If you add or remove cards, make sure to also update:

- `CARD_IMAGES`
- `TOTAL_CARDS`

## Running It

This is a static site, so you can open `index.html` directly in a browser or host the folder on any simple static hosting service.

For the cleanest QR behavior, it is best to host it from a real local or remote web server rather than opening the file via `file://`.

## Admin View

The admin page is the default page. It lets you:

- display the QR code for guests to scan
- reset the rotation counter back to card 1

## User View

After scanning, the user sees:

- the assigned bingo card image
- a button to download that image

## Notes

- The QR code is generated in the browser using `qrcodejs`.
- The rotation is sequential, not random.
- Resetting the counter makes the next scan receive card 1 again.
