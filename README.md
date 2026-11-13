# Air Rocket Flight Lab

Design a 3D-printed air rocket in Tinkercad, check whether it's stable, and predict how it flies off a compressed-air launcher before you print it.

Inspired by NASA Glenn's [RocketModeler](https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/rocketmodeler/), rebuilt for 3D-printed rockets on an [Air Rocket Works](https://www.airrocketworks.com/) style launcher. Not affiliated with NASA or Air Rocket Works.

**Live app:** https://YOUR-USERNAME.github.io/air-rocket-flight-lab/

## For students

1. In Tinkercad, design your rocket with a **21 mm hole** up the tail so it slides onto the launch tube.
2. Export it: **Export → .STL**.
3. Open the app and drop your STL onto **Your rocket**.
4. Check the **stability** badge. Aim for 1 to 3 calibers. If it says unstable, add nose weight or bigger fins.
5. Change the launch angle and drag, then press **Launch**. Use **Save to compare** to test one change at a time.
6. After printing, weigh your rocket and enter the real mass.

## For teachers

Open **Launcher setup** and enter your class launcher's values: launch pressure, tank volume (fill the empty tank with water to measure it), and launch tube length. To make your values the defaults for everyone, edit the `value="..."` attributes on those inputs in `index.html`.

Calibrate with real flights: measure peak heights with a clinometer, then adjust **launcher efficiency** and **drag coefficient** until predictions match.

### Install as an app

On a Chromebook or in Chrome, open the live link and choose **Install** in the address bar (or menu → Cast, save and share → Install page as app). After the first visit it works offline, so it runs at the launch field without Wi-Fi.

## How the model works

- **Shape:** the STL is sliced into 240 cross sections along its long axis to find body diameter, side silhouette, fins and the launch bore.
- **Center of pressure:** Barrowman equations using the detected fins (count, span, root and tip chord). Falls back to the cardboard cutout method if no fins are found.
- **Mass and center of gravity:** estimated from wall thickness and infill, or from a weighed mass.
- **Launch:** tank air expands while pushing on the 21 mm bore area for the bore depth or tube length, whichever is shorter.
- **Flight:** gravity plus quadratic drag in 2D, stepped every millisecond. Unstable rockets are modeled as tumbling.

## Publishing on GitHub Pages

1. Create a **public** repository (Pages on private repos needs a paid plan).
2. Upload **every file and folder** here, keeping the structure. `index.html` must sit at the top level of the repo, not inside a subfolder.
3. **Settings → Pages → Build and deployment:** Source **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.
4. Wait 1–2 minutes, then check the **Actions** tab for a green check. The link appears at the top of the Pages settings.

### If Pages doesn't work

- **404 page:** `index.html` isn't at the repo root, the branch or folder in Pages settings is wrong, or the first deploy hasn't finished. Check the Actions tab.
- **Page loads but looks unstyled or the 3D view is missing:** a folder didn't upload. GitHub's web uploader needs the folders dragged in, not just the files inside them. Make sure `vendor/`, `fonts/` and `icons/` exist in the repo.
- **File name errors:** GitHub Pages is case-sensitive. `Index.html` or `Vendor/` will not work.
- **Old version still showing after an update:** bump `VERSION` in `sw.js`, push, then reload the page twice.
- **Odd behavior with folders that start with an underscore:** the empty `.nojekyll` file turns off Jekyll processing. Keep it in the repo root.

## License

MIT. See `LICENSE`. Bundled three.js (MIT) and Barlow fonts (SIL OFL 1.1) keep their own licenses.
