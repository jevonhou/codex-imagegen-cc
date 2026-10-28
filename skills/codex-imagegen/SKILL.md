---
name: codex-imagegen
description: Generate image assets for design work with the locally installed Codex CLI. Use when Claude needs a raster image for a website, presentation, prototype, cover, illustration, or other visual deliverable and Codex image generation is available. Prefer editable code or vectors for interface controls, diagrams, and simple graphics.
---

# Codex Imagegen

Use the local Codex CLI to generate raster assets when an image would materially improve the user's design. Claude remains responsible for the design and integrates the resulting assets into the deliverable.

## Decide what to generate

- Respect the user's chosen assets, visual direction, cost limits, and requested scope. Do not replace existing imagery or invent additional assets without a reason.
- Good candidates include photographic or illustrated scenes, product concepts, textures, backgrounds, and thumbnails. A temporary placeholder alone is not a reason to generate an image if the user has asked for placeholders or provided real assets.
- Keep interface text, controls, charts, diagrams, and simple shapes editable in their appropriate native format. Generated product images or people are illustrative; do not present them as documentary evidence of real products, people, or events.
- For each needed image, decide its purpose, subject, visual style, composition, aspect ratio, and any space needed for overlay text. Avoid embedding UI text in an asset when it belongs in the interface.

## Generate and use

1. Confirm that `codex` is available and authenticated (`codex --version`, `codex login status`), and that image generation is available in the active Codex environment. The user may need to install, sign in, enable the feature, or grant command permissions. Do not ask them to share credentials.
2. Run Codex from the project directory. Give it the image brief and an explicit destination inside the project; request a new filename and do not overwrite existing assets without authorization. For example:

   ```sh
   codex exec --skip-git-repo-check -s workspace-write \
     'Use your image generation tool to create a landscape hero image: a quiet mountain lake at dawn, soft natural light, no text. Copy the result to ./images/mountain-lake-hero.png if that path does not already exist, and report the absolute path.'
   ```

   Allow enough time for generation and honor the host's permissions. A Codex invocation can consume usage or incur costs depending on the account and configuration. Group related requests when useful, but split them when separate iteration, failures, or user constraints make that more reliable.
3. Verify the reported file exists, inspect the image, and check its subject, composition, quality, and fit for the intended placement. Revise if necessary within the user's scope.
4. Reference the saved project asset in the deliverable. Keep any interface text and interaction editable. Tell the user where the asset was saved and that it is AI-generated when that matters to the context.

If Codex, authentication, image generation, permissions, quota, or the output is unavailable, explain the specific failure. Use an existing authorized asset or a clearly labeled placeholder only when appropriate; do not claim generation succeeded. Do not retry indefinitely or switch to a paid API path without the user's authorization.
