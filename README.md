# animegirly-imagen

Companion repo for [AnimeGirly](https://github.com/WestonGFX/AnimeGirly) — generate anime character images and videos using Google Gemini, EasyDiffusion (Stable Diffusion), and ChatGPT.

## What This Does

- Generate 2D character art, scenes, and reference sheets for AnimeGirly characters
- Multiple backends: Google Gemini API (cloud), EasyDiffusion/Stable Diffusion (local GPU), ChatGPT (copy-paste)
- Video generation via Google Veo 3.1
- Prompt library with 30 pre-built prompts for Genki (kitsune fox spirit girl)
- Character keyword swapper for adapting prompts to other characters

## Characters

| Character | Archetype | Visual Signature |
|-----------|-----------|-----------------|
| **Genki** | Kitsune fox spirit, genki | Orange-red hair with white tips, amber-gold eyes, fox ears, fluffy tail |
| **Neciridae** | Fox, tsundere e-girl | Long dark hair, heterochromia eyes, cat-eye eyeliner, alt-fashion |
| **Sable (Kuroha)** | Sadodere, cyberpunk | (from waifu-rt3d character bible) |
| **Shiori, Rin, Ayane, Hana, Mika** | Various archetypes | (from waifu-rt3d character bible) |

## Quick Start

### Google Colab (easiest)
1. Open `quickstarts/Batch_mode.ipynb` in Colab (link in notebook)
2. Add your Google API key to Colab Secrets as `GOOGLE_API_KEY`
3. Upload reference images to `/content/`
4. Run cells top-to-bottom

### Local CLI Tools
These live in the main AnimeGirly repo under `tools/`:

```bash
# Install dependency
pip install google-genai requests

# Generate an image with Gemini
python tools/gemini_imagen.py --prompt "Genki waving hello"

# Generate with EasyDiffusion (needs Windows PC running)
python tools/easydiffusion_gen.py --prompt "anime kitsune girl, cel shaded"

# Batch generation
python tools/gemini_imagen.py --batch prompts.txt --output-dir ./output/

# Video generation
python tools/gemini_imagen.py --video --prompt "Genki dancing at shrine festival"
```

### Web UI (recommended for regular use)
```bash
pip install flask google-genai requests
python tools/imagen_server.py
# Opens http://localhost:8080 with visual prompt editor and gallery
```

## Prompt Format

Prompts follow this structure for best results:
```
[Character name], [archetype description], [visual details from reference sheet],
[scene/setting], [action/pose], [lighting], [art style keywords],
[framing], [loop instructions if animation]
```

Example:
```
Genki, anime kitsune fox spirit girl, orange-red hair with white tips,
amber-gold eyes, fox ears, fluffy tail, standing in a cozy modern bedroom
with shrine-inspired decor, playful smile, one hand raised in greeting,
soft orange and blue ambient lighting, polished anime cel-shaded style,
centered medium shot, visually memorable
```

## Adapting Prompts for Other Characters

Replace Genki-specific keywords with another character's visuals:
- "orange-red hair with white tips" → "[character's hair]"
- "amber-gold eyes" → "[character's eyes]"
- "fox ears, fluffy tail" → "[character's distinctive features]"
- "shrine-inspired decor" → "[character's environment]"

The web UI has a built-in keyword swapper for this.

## Backends

| Backend | Type | Cost | Best For |
|---------|------|------|----------|
| Gemini 2.5 Flash Image | Cloud API | Free tier + paid | Quick iterations, consistent style |
| Veo 3.1 | Cloud API | Paid | Video generation (5-8s clips) |
| EasyDiffusion | Local GPU | Free | High volume, custom SD models, no rate limits |
| ChatGPT | Web/Desktop | Subscription | One-off images, DALL-E quality |

## Repository Structure

```
quickstarts/
  Batch_mode.ipynb    # Google Colab notebook for Gemini batch image gen
```

Local tools are in the main AnimeGirly repo under `tools/`.

## Related

- [AnimeGirly](https://github.com/WestonGFX/AnimeGirly) — Main app (private)
- [EasyDiffusion](https://github.com/easydiffusion/easydiffusion) — Local Stable Diffusion
- [Google AI Studio](https://aistudio.google.com/) — Gemini API dashboard
