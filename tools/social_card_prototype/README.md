# Social Card Prototype

Prototype generator for learn.arm.com social/Open Graph cards with updated branding and name of the content directly in the image. It reads a Learning Path or install guide Markdown file, pulls the `title` from front matter, applies the content type label, and writes `output.webp`.

You'll need these python files installed:
```bash
pip install playwright Pillow
python -m playwright install --only-shell chromium
```

Test from the repo root:

```bash
python tools/social_card_prototype/generate.py content/install-guides/ambaviz.md
python tools/social_card_prototype/generate.py content/learning-paths/embedded-and-microcontrollers/advanced_soc
```

Open `tools/social_card_prototype/output.webp` to inspect the result.

Exact brand rendering still needs a font solution for `fonts/Aeonik-Medium.otf` and `fonts/AeonikFono-Regular.otf`, which I have from our branding team but we are unable to host in the OSS repo on GitHub due to licensing with the owners of Aeonik. The current system font fallbacks are close enough for now.
