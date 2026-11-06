# Jaipur Startup Arena

An interactive 3D map of Jaipur's startup ecosystem. Spin the globe, fly into Jaipur, and explore startups on a real street network, with moving traffic and pedestrians. No sign-up, no backend, no build step.

**Live demo:** https://jprstartups.vercel.app/

> Best viewed on a desktop or a recent phone. Drag to rotate, scroll or pinch to zoom, and click a marker for the company website.

## Features

- **Globe to city:** a textured Earth that flies to Jaipur, with a camera that tilts as you zoom in.
- **Real road network:** about 200,000 road segments of Jaipur drawn as glowing streets.
- **Startup markers:** colour-coded by sector. Search, filter by sector, and click a marker for details and a link to the company website.
- **Street-level life:** zoom all the way in to see motorbikes with riders, cars, auto-rickshaws, buses and walking pedestrians moving along the real roads.
- **Ridge relief:** soft hill shading and contour lines around the Aravalli ridges.
- **Mobile friendly:** lighter graphics, a collapsible bottom list and pinch to zoom.

## Run locally

It is a single self-contained file.

```bash
# option 1: just open index.html in your browser
# option 2: serve it locally
python3 -m http.server 8000
# then visit http://localhost:8000
```

The page loads three.js (r128) from the cdnjs CDN, so it needs an internet connection.

## Deploy

The live site runs on **Vercel**: https://jprstartups.vercel.app/

**Vercel (recommended):**

1. Push this repository to GitHub.
2. On [vercel.com](https://vercel.com), click **Add New → Project** and import the repository.
3. Leave the framework preset as **Other**, keep the defaults (no build command, no output directory), and click **Deploy**.
4. Every later `git push` to `main` redeploys automatically.

**GitHub Pages (alternative):** go to **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.

## Add or edit startups

Open `index.html` and find the `DATA` list near the top of the script. Each entry looks like this:

```js
{"n":"Company Name","s":"SaaS","a":"Malviya Nagar","lat":26.855,"lng":75.817,
 "u":"https://example.com","d":"One-line description.","r":["Software Engineer","Designer"]}
```

| Field | Meaning |
|-------|---------|
| `n` | Company name |
| `s` | Sector. Sector colours are set in the `SCOL` object (add a new colour there for a new sector) |
| `a` | Neighbourhood shown on the card |
| `lat`, `lng` | Approximate location |
| `u` | Website or careers page |
| `d` | Short description |
| `r` | Teams or roles to watch |

Markers are nudged slightly apart so they do not overlap, and are kept inside the city boundary, so their positions are approximate.

## How it works

- **three.js** for the globe, ground, markers, vehicles and people.
- **Road graph:** Jaipur's road network (nodes and edges) is embedded in the page. Vehicles and pedestrians walk this graph in real time near the camera.
- **Earth imagery:** NASA Blue Marble textures, embedded as images.
- **Road image:** the street network is also pre-rendered into a texture for the zoomed-out city view.
- **Ward map:** Jaipur's municipal ward boundaries form the city outline and zone labels.

## Limitations

- Startup locations are approximate (neighbourhood level), not exact office addresses.
- The "teams to watch" are not verified live job openings. Always check the company's own site.
- The relief is stylised, drawn around the approximate positions of the Aravalli ridges (Nahargarh, Jaigarh, Amer, Galta, Jhalana). It is **not** survey elevation data.
- Vehicles and pedestrians are a simulation on real roads, not live data, and are drawn larger than life so they are visible.
- There are no buildings in the street view.
- The page is large (about 11 MB) because the map data is embedded.

## Repository structure

```
.
├── index.html   # the whole app (HTML + JS + embedded data)
└── README.md
```

## Data sources and credits

- **Road network:** © OpenStreetMap contributors (ODbL). The road graph was taken from the [MinGraph](https://github.com/aryy8/MinGraph) project's Jaipur extract.
- **Ward boundaries:** [DataMeet Municipal Spatial Data](https://github.com/datameet/Municipal_Spatial_Data).
- **Earth imagery:** NASA Blue Marble (public domain), via the [three-globe](https://github.com/vasturiano/three-globe) example images.
- **3D engine:** [three.js](https://threejs.org).
- **Startup list:** compiled from public Jaipur startup lists.

Please keep the attribution line in the page footer. If you reuse the map data, check the licence terms of each source above.

This project is not affiliated with any of the companies shown.
