# GeoQuiz

A geography quiz app. Runs in any browses, phone or laptop.:)

---

## Folder structure

```
geoQuiz/
├── index.html
├── maps/
│   └── belgium-provinces.svg     ← your SVG maps go here
└── data/
    └── belgium-provinces.json    ← matching JSON data files go here
```

---

## How to add a new map

### 1. Prepare your SVG in Inkscape

Each region needs a unique **ID** on its `<path>` element.

In Inkscape:
1. Click a region
2. Go to **Object → Object Properties**
3. Set the **ID** field (e.g. `BE-VWV` for West Flanders)
4. Repeat for all regions
5. Save as **Plain SVG** (not Inkscape SVG)

> If you're exporting from QGIS, use the **Processing Toolbox** or a Python script to add a `id` attribute from a field like `NAME_1`.

### 2. Create the JSON data file

```json
{
  "name": "My Map Name",
  "regions": {
    "BE-VWV": "West Flanders",
    "BE-VOV": "East Flanders",
    "BE-VAN": "Antwerp"
  }
}
```

The keys must exactly match the SVG path IDs.

### 3. Add to index.html (optional, for built-in maps)

In `index.html`, find `BUILT_IN_MAPS` and add an entry:

```javascript
{
  id: 'my-map',
  name: 'My Map',
  svgFile: 'maps/my-map.svg',
  jsonFile: 'data/my-map.json'
}
```

Or just use the **Import** button in the app to load files directly from your device.

---

## Deploy to GitHub Pages (free hosting)

1. Create a new repo at github.com (e.g. `geoquiz`)
2. Upload all files (keep the folder structure)
3. Go to repo **Settings → Pages**
4. Under **Source**, select `main` branch, `/ (root)`
5. Save → your app is live at `https://yourusername.github.io/geoquiz`

Open that URL on your phone. Add it to your home screen (Share → Add to Home Screen on iOS, or the browser menu on Android) for an app-like experience.

---

## How the review feature works

After each quiz:
- All regions you got **wrong** are saved
- The **"Review wrong answers"** button starts a new quiz with **only those regions**
- After that review quiz, you can review again — drilling down until you get them all right
- This chains exactly like Seterra's review mode

---

## Tips

- SVG paths without an `id` are ignored by the quiz
- The app warns you if your JSON IDs don't match any SVG IDs
- You can import maps directly on your phone — no laptop needed
- Works fully offline once loaded (no internet required after first load)
