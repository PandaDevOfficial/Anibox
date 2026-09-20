<div align="center">

# anibox

A free, fast anime roleplay & reaction asset ecosystem for bots and web apps.

[![Discord Support](https://img.shields.io/discord/YOUR_DISCORD_ID?color=5865F2&label=Support%20Server&logo=discord&logoColor=white)](https://discord.gg/YOUR_INVITE_CODE)
[![npm version](https://img.shields.io/npm/v/anibox?color=black&style=flat)](https://www.npmjs.com/package/anibox)
[![CDN Status](https://img.shields.io/badge/CDN-Cloudflare%20Pages-orange)](https://cdn-anibox.pages.dev)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

[CDN Endpoint](https://cdn-anibox.pages.dev) • [SDK Repo](https://github.com/PandaDevOfficial/anibox-sdk) • [Asset Repo](https://github.com/PandaDevOfficial/Anibox-CDN) • [Discord Server](https://discord.gg/YOUR_INVITE_CODE)

</div>

---

## What is Anibox?

Anibox is an open-source media stack designed for Discord roleplay commands (`/hug`, `/pat`, `/slap`, `/dance`) and reaction features. Instead of relying on rate-limited public APIs or hosting hundreds of GIFs yourself, Anibox provides:

1. **[Anibox CDN](https://github.com/PandaDevOfficial/Anibox-CDN)**: 682 curated anime GIFs sorted across 61 categories, served over Cloudflare Edge with global caching and open CORS.
2. **[Anibox SDK](https://github.com/PandaDevOfficial/anibox-sdk)**: A lightweight, zero-dependency client with native TypeScript types and synchronous URL resolution.

---

## Repositories

| Repository | Description | Link |
| :--- | :--- | :--- |
| **Anibox-CDN** | Raw GIF assets, manifest index, and Cloudflare Pages configuration. | [GitHub](https://github.com/PandaDevOfficial/Anibox-CDN) |
| **anibox-sdk** | Node.js & browser client library published on npm. | [GitHub](https://github.com/PandaDevOfficial/anibox-sdk) |

---

## Quick Start (SDK)

### 1. Install

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

// Get a specific GIF
const slap = anibox.get("slap", 3);

// List all GIFs in a category
const dances = anibox.list("dance");
```

### 3. Discord.js v14 Example

```javascript
import { SlashCommandBuilder, EmbedBuilder } from "discord.js";
import { anibox } from "anibox";

export const data = new SlashCommandBuilder()
  .setName("hug")
  .setDescription("Hug someone")
  .addUserOption(o => o.setName("target").setDescription("User to hug").setRequired(true));

export async function execute(interaction) {
  const target = interaction.options.getUser("target");
  const gifUrl = anibox.random("hug");

  const embed = new EmbedBuilder()
    .setColor(0xff69b4)
    .setDescription(`${interaction.user} hugged ${target}!`)
    .setImage(gifUrl)
    .setFooter({ text: "Powered by Anibox" });

  await interaction.reply({ embeds: [embed] });
}
```

---

## Direct CDN Usage

If you prefer fetching without the SDK, consume the endpoints directly:

```text
# Pattern
https://cdn-anibox.pages.dev/{category}/{number}.gif

# Examples
https://cdn-anibox.pages.dev/hug/1.gif
https://cdn-anibox.pages.dev/dance/4.gif
https://cdn-anibox.pages.dev/pat/10.gif

# Manifest / Index of all categories and counts
https://cdn-anibox.pages.dev/index.json
```

---

## Available Categories (61)

`airkiss`, `angrystare`, `bite`, `bleh`, `brofist`, `celebrate`, `cheers`, `clap`, `confused`, `cool`, `cry`, `cuddle`, `dance`, `drool`, `evillaugh`, `facepalm`, `handhold`, `happy`, `headbang`, `hug`, `kiss`, `laugh`, `lick`, `love`, `mad`, `nervous`, `nom`, `nuzzle`, `nyah`, `pat`, `peek`, `pinch`, `poke`, `pout`, `punch`, `sad`, `scared`, `shout`, `shrug`, `shy`, `sigh`, `sip`, `slap`, `sleep`, `slowclap`, `smack`, `smile`, `sneeze`, `sorry`, `stare`, `surprised`, `sweat`, `thumbsup`, `tickle`, `tired`, `wave`, `wink`, `woah`, `yawn`, `yay`, `yes`.

---

## Support & Community

Need help integrating Anibox into your bot, want to request a category, or have questions?

* Join the **[Discord Support Server](https://discord.gg/YOUR_INVITE_CODE)**.
* Open an issue in [Anibox-CDN](https://github.com/PandaDevOfficial/Anibox-CDN/issues) for broken GIFs or asset submissions.
* Open an issue in [anibox-sdk](https://github.com/PandaDevOfficial/anibox-sdk/issues) for bug reports or feature requests in the library.

---

## License

MIT © [PandaDevOfficial](https://github.com/PandaDevOfficial).
