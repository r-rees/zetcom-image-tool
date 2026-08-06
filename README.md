# zetcom image tool

Browser-based image cropper & social-card composer for zetcom.
**Live:** https://r-rees.github.io/zetcom-image-tool/

Upload any image (any format / ratio), pick a target — relaunch panel (hero,
image_text, sticky, benefits, teaser, up_next, panel_image), social format
(OG, LinkedIn link/post/banner, newsletter header), logo preset, or a custom
pixel size — then crop / zoom / rotate / flip to the exact target ratio and
export **WebP / JPG / PNG** at the right dimensions and quality.

Includes a CD-correct **text composer** (eyebrow · title · subline · meta ·
CTA button), a draggable/recolourable **pixel-square decor** in the zetcom
brand palette, and the zetcom logo (light / dark / custom). DM Sans and the
logos are embedded, so the page is fully self-contained and works offline.

Everything runs client-side — images never leave the browser.

---

## How this repo is fed

Generated from the zetcom vault (`tools/apps/zetcom-image-cropper-tool.html`).
**Do not edit `index.html` here** — it is overwritten from the vault by
`tools/publish-image-cropper.ps1`, or by the git hooks in `tools/git-hooks/`
on every local commit that touches the tool.

Pages serves the repo root from `main` ("pages build and deployment"). Every
push to `main` queues a deployment, whatever the push changed.

## When the live page stays old

The published `index.html` and the live page are two different things. Check in
this order:

1. **Is the file here current?** Compare its hash with the vault:
   `sha256sum index.html` against
   `sha256sum tools/apps/zetcom-image-cropper-tool.html` in the vault.
   Identical means the publish step worked and the problem is downstream.
2. **Did a deployment run and succeed?** Actions tab, workflow
   *pages build and deployment*. A push without a run, or a run in red, is the
   answer. Deployments can hang: on 06.08.2026 one sat in
   `deployment_in_progress` for ten minutes and was cancelled with
   `Timeout reached, aborting!`, so the site kept serving the previous build
   although the file here was already correct. That is a GitHub-side stall, not
   a content problem — re-run the job, or push again to queue a fresh
   deployment.
3. **Only then suspect the browser.** Hard reload (Ctrl + F5), then a private
   window. The file is over half a megabyte and always has the same name, so it
   caches well.
