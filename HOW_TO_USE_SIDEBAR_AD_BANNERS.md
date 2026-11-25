# How to Use the `sidebar-ad-banners` Skill

**Skill Name:** `sidebar-ad-banners`  
**Skill Location:** `.agents/skills/sidebar-ad-banners/SKILL.md`  
**Sample Data:** `.agents/skills/sidebar-ad-banners/references/sample-campaigns.json`

---

## 1. Starting the Skill

You can invoke the skill in chat with a prompt such as:
- *"Use the `sidebar-ad-banners` skill to design sidebar ads for my company."*
- *"Create website sidebar ad banners in Figma."*

When the skill starts without an existing brief, it will:
1. Summarize what it will generate in Figma (`300×600`, `300×250`, `160×600`).
2. Explain the expected input format.
3. Prompt you for your requirement document or structured brief.

---

## 2. Expected Input Format

Paste a requirement document, share a link/file, or fill in this template:

```markdown
### Sidebar Ad Banner Requirement Brief
- **Brand Name**: Your Company / Product
- **Logo / Visuals**: Figma node/file link, image description, or "simple geometric mark"
- **Brand Colors**:
  - Background: #HEX (and optional secondary gradient #HEX)
  - Accent / CTA Button: #HEX
  - Text Primary / Muted: #HEX / #HEX
- **Font Family**: e.g., Plus Jakarta Sans, Inter, DM Sans
- **Campaign Copy**:
  - Badge (optional): e.g., FREE TRIAL, 25% OFF, AD
  - Headline (≤ 6 words): Short punchy headline
  - Subheadline (1 sentence): Value proposition
  - Metric / Proof Card (for tall banners): e.g., +148% Campaign Lift
  - CTA Copy: e.g., Start Free Trial →, Shop Now →
  - Trust Microcopy (optional): e.g., No card required
- **Target Sidebar Sizes**: 300×600 Half Page, 300×250 Medium Rectangle, 160×600 Wide Skyscraper
- **Figma Destination**: Existing Figma file URL or "Create new file"
```

> **Tip:** To test the skill without writing a brief, ask: *"Test `sidebar-ad-banners` with the sample campaigns."*

---

## 3. Standard Sidebar Sizes Generated

| Format | Dimensions | Best Placement |
| :--- | :--- | :--- |
| **Half Page** | `300 × 600` px | Primary right/left website sidebar (highest visibility) |
| **Medium Rectangle** | `300 × 250` px | Compact sidebar slot or inline article rail |
| **Wide Skyscraper** | `160 × 600` px | Narrow website sidebars |

---

## 4. Exporting & Using the Banners on Websites

1. **Open your Figma file** and select any `Sidebar Ad` frame (each frame has exact fixed dimensions and `clipsContent` enabled).
2. **Export from Figma**:
   - In the right-hand **Export** panel, choose **PNG** (at `1x` for exact pixel size or `2x` for Retina/HiDPI displays) or **JPG** (for smaller ad-network file sizes).
3. **Deploy to Websites or Ad Networks**:
   - **Ad Networks (Google Ads / Programmatic)**: Upload the exported `300×600`, `300×250`, and `160×600` assets directly as Display Ad creatives and set your landing page URL.
   - **Direct Website / Blog Sidebar**: Upload the image to your CMS (WordPress, Webflow, etc.) or embed it in a sidebar widget:

```html
<a href="https://yourcompany.com/landing-page" target="_blank" rel="noopener sponsored">
  <img
    src="/ads/sidebar-300x600.png"
    alt="YourBrand — Grow Your Conversions 3x Faster"
    width="300"
    height="600"
  />
</a>
```

---

## 5. Using This Skill with Antigravity or Claude Code

Make sure the **Figma MCP server** is installed and signed in on your target tool so it can create and edit Figma files.

### Option A: Antigravity
1. **Workspace install** (already set up if you clone this repo):
   ```bash
   git clone https://github.com/soorajtrs/figma_banner_gen.git
   ```
   Antigravity automatically discovers `.agents/skills/sidebar-ad-banners/SKILL.md` in the workspace.
2. **Global install** (to use across all projects):
   ```bash
   mkdir -p ~/.gemini/config/skills
   cp -r .agents/skills/sidebar-ad-banners ~/.gemini/config/skills/
   ```
3. **Run it**: Open Antigravity and prompt:
   > *"Use the `sidebar-ad-banners` skill to create sidebar ads for my company."*

### Option B: Claude Code
1. **Project install** (copy into `.claude/skills/` in your project):
   ```bash
   mkdir -p .claude/skills
   cp -r .agents/skills/sidebar-ad-banners .claude/skills/
   ```
2. **Global install** (to use in any repository):
   ```bash
   mkdir -p ~/.claude/skills
   cp -r .agents/skills/sidebar-ad-banners ~/.claude/skills/
   ```
3. **Connect Figma MCP** in Claude Code (if not already configured):
   ```bash
   claude mcp add --transport http figma https://mcp.figma.com/mcp
   ```
4. **Run it**: Start Claude Code and invoke `/sidebar-ad-banners` or prompt:
   > *"Use the `sidebar-ad-banners` skill to design website sidebar ads in Figma."*

