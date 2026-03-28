FULL_REPO_SETUP.md

const fetchMovies = require("./fetch-movies");
const generateContent = require("./generate-content");
const generateHooks = require("./generate-hooks");

async function run() {
  await fetchMovies();
  generateContent();
  generateHooks();
  console.log("🚀 FULL AI PIPELINE COMPLETE");
}

run();

const fs = require("fs");
const axios = require("axios");
require("dotenv").config();

const API_KEY = process.env.TMDB_API_KEY;

async function fetchMovies() {
  try {
    const res = await axios.get(
      `https://api.themoviedb.org/3/trending/movie/day?api_key=${API_KEY}`
    );

    const data = res.data.results.slice(0, 10).map((m) => ({
      title: m.title,
      desc: m.overview,
      image: "https://image.tmdb.org/t/p/w500" + m.poster_path,
      link: process.env.AFFILIATE_LINK
    }));

    fs.writeFileSync("../data/movies.json", JSON.stringify(data, null, 2));
    console.log("✅ Movies fetched");
  } catch (err) {
    console.error(err);
  }
}

module.exports = fetchMovies;

const fs = require("fs");

function generateContent() {
  const data = JSON.parse(fs.readFileSync("../data/movies.json"));

  let content = "🔥 Top Trending Movies\n\n";

  data.forEach((m, i) => {
    content += `${i + 1}. ${m.title}\n${m.desc}\n\n`;
  });

  fs.writeFileSync("../data/content.txt", content);
  console.log("✅ Content generated");
}

module.exports = generateContent;

const fs = require("fs");

function generateHooks() {
  const hooks = [
    "Stop scrolling — watch this now",
    "Top trending movies today",
    "You missed these hidden gems",
    "These movies are going viral",
    "Don't watch anything before this list"
  ];

  fs.writeFileSync("../data/hooks.json", JSON.stringify(hooks, null, 2));
  console.log("✅ Hooks generated");
}

module.exports = generateHooks;

const axios = require("axios");
require("dotenv").config();

async function generateAIHooks(prompt) {
  const res = await axios.post(
    "https://api.openai.com/v1/chat/completions",
    {
      model: "gpt-4o-mini",
      messages: [{ role: "user", content: prompt }]
    },
    {
      headers: {
        Authorization: `Bearer ${process.env.OPENAI_API_KEY}`
      }
    }
  );

  return res.data.choices[0].message.content;
}

module.exports = generateAIHooks;

{
  "name": "ai-business-os",
  "version": "1.0.0",
  "dependencies": {
    "axios": "^1.6.0",
    "dotenv": "^16.0.0"
  }
}

<!DOCTYPE html>
<html>
<head>
  <title>AI Movie Engine</title>
</head>
<body>

<h1>🔥 Trending Movies</h1>
<div id="app"></div>

<script>
async function load(){
  const res = await fetch("../data/movies.json");
  const data = await res.json();

  document.getElementById("app").innerHTML =
    data.map(m => `
      <div>
        <h2>${m.title}</h2>
        <img src="${m.image}" width="200"/>
        <p>${m.desc}</p>
        <a href="${m.link}" target="_blank">Watch Now</a>
      </div>
    `).join("");
}

load();
</script>

</body>
</html>

<h1>📊 Dashboard</h1>
<div id="stats"></div>

<script>
const stats = [
  {name:"Views", value:12000},
  {name:"CTR", value:"6.5%"},
  {name:"Revenue", value:"$120"}
];

document.getElementById("stats").innerHTML =
  stats.map(s=>`<div>${s.name}: ${s.value}</div>`).join("");
</script>

name: AI Auto System

on:
  schedule:
    - cron: "0 */6 * * *"
  workflow_dispatch:

jobs:
  run:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - uses: actions/setup-node@v3
        with:
          node-version: 18

      - run: cd backend && npm install

      - run: node backend/main.js

      - run: |
          git config user.name "bot"
          git config user.email "bot@email.com"
          git add .
          git commit -m "auto update" || echo "no changes"
          git push

[]

Generate 10 viral hooks for movie content.

Rules:
- Short
- Emotional
- Curiosity-driven
- Pattern interrupt
- Clickbait but not spam

Format:
1.
2.
3.

Generate SEO blog content:

Keyword: {{movie}}

Include:
- H1
- H2 sections
- Description
- CTA

# 🚀 AI Business OS

Automated AI content + traffic + monetization engine.

## Setup

1. Clone repo
2. Add .env
3. Run:
   cd backend
   npm install
   node main.js

## Automation
Runs every 6 hours via GitHub Actions

## Deploy
Frontend → Netlify or Vercel

## Monetization
- Affiliate links
- CPA
- Ads





