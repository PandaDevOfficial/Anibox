<div align="center">

# anibox

A free, high-performance anime roleplay & reaction media ecosystem for bots and web apps.

[![Discord Support](https://img.shields.io/discord/1078772023531126904?color=5865F2&label=Support%20Server&logo=discord&logoColor=white)](https://discord.gg/QgZ6kvANQc)
[![npm version](https://img.shields.io/npm/v/anibox?color=black&style=flat)](https://www.npmjs.com/package/anibox)
[![CDN Status](https://img.shields.io/badge/CDN-Cloudflare%20Pages-orange)](https://cdn-anibox.pages.dev)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

[Cloudflare CDN](https://cdn-anibox.pages.dev) • [npm Package](https://www.npmjs.com/package/anibox) • [Discord Support](https://discord.gg/QgZ6kvANQc) • [Report Issue](https://github.com/PandaDevOfficial/Anibox/issues)

</div>

---

## What is Anibox?

Anibox is an asset ecosystem designed for Discord bot roleplay commands (`/hug`, `/pat`, `/slap`, `/dance`) and reaction features. Instead of relying on rate-limited third-party APIs or self-hosting heavy media files, Anibox provides:

* **Cloudflare Edge CDN**: 682 hand-curated anime GIFs across 61 categories, delivered globally with open CORS and permanent edge caching.
* **Official npm Package (`anibox`)**: A zero-dependency client with native TypeScript types and instant synchronous URL resolution.

---

## 📦 Getting Started (npm)

### 1. Installation

```bash
npm install anibox
# or
pnpm add anibox
# or
yarn add anibox
```

### 2. Basic Usage

```javascript
import { anibox } from "anibox";

// Get a random GIF URL (synchronous, 0ms latency)
const gif = anibox.random("hug");
console.log(gif);
// => "https://cdn-anibox.pages.dev/hug/7.gif"

// Get a specific GIF by number
const slap = anibox.get("slap", 3);

// List all GIFs in a category
const dances = anibox.list("dance");
```

### 3. Discord.js v14 Bot Example

```javascript
import { SlashCommandBuilder, EmbedBuilder } from "discord.js";
import { anibox } from "anibox";

export const data = new SlashCommandBuilder()
  .setName("hug")
  .setDescription("Give someone a warm hug!")
  .addUserOption(opt =>
    opt.setName("target").setDescription("User to hug").setRequired(true)
  );

export async function execute(interaction) {
  const target = interaction.options.getUser("target");
  const gifUrl = anibox.random("hug");

  const embed = new EmbedBuilder()
    .setColor(0xff69b4)
    .setDescription(`${interaction.user} hugged ${target}! (っ´ω\`)っ`)
    .setImage(gifUrl)
    .setFooter({ text: "Powered by Anibox" });

  await interaction.reply({ embeds: [embed] });
}
```

---

## 🌐 Direct CDN Usage

If you prefer consuming raw URLs without installing the library:

```text
# URL Pattern
https://cdn-anibox.pages.dev/{category}/{number}.gif

# Examples
https://cdn-anibox.pages.dev/hug/1.gif
https://cdn-anibox.pages.dev/dance/4.gif
https://cdn-anibox.pages.dev/pat/10.gif

# Manifest / Index (all categories and counts)
https://cdn-anibox.pages.dev/index.json
```

---

## 🎭 Available Categories (61)

`airkiss`, `angrystare`, `bite`, `bleh`, `brofist`, `celebrate`, `cheers`, `clap`, `confused`, `cool`, `cry`, `cuddle`, `dance`, `drool`, `evillaugh`, `facepalm`, `handhold`, `happy`, `headbang`, `hug`, `kiss`, `laugh`, `lick`, `love`, `mad`, `nervous`, `nom`, `nuzzle`, `nyah`, `pat`, `peek`, `pinch`, `poke`, `pout`, `punch`, `sad`, `scared`, `shout`, `shrug`, `shy`, `sigh`, `sip`, `slap`, `sleep`, `slowclap`, `smack`, `smile`, `sneeze`, `sorry`, `stare`, `surprised`, `sweat`, `thumbsup`, `tickle`, `tired`, `wave`, `wink`, `woah`, `yawn`, `yay`, `yes`.

---

## 💬 Support & Community

Need help integrating Anibox into your project, want to suggest new categories, or found a broken GIF?

* Join our **[Discord Support Server](https://discord.gg/QgZ6kvANQc)**.
* Open an issue in our **[GitHub Issues](https://github.com/PandaDevOfficial/Anibox/issues)** tracker for bug reports, broken GIF replacements, or library feedback.

---

## 📄 License

MIT © [PandaDevOfficial](https://github.com/PandaDevOfficial).
