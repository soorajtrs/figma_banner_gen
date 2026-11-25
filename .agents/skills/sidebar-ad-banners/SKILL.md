---
name: sidebar-ad-banners
description: "Design and generate website sidebar advertisement banners in Figma in standard IAB sidebar sizes (300×600 Half Page, 300×250 Medium Rectangle, 160×600 Wide Skyscraper). Use when the user asks to create sidebar ads, display banners, or marketing banner sets in Figma."
---

# Website Sidebar Ad Banner Generator (Figma)

Use this skill to design export-ready website sidebar advertisement banners directly in Figma.

## Step 1: Startup Summary & Requirement Prompt (Mandatory First Step)

When the user invokes this skill without already providing a complete campaign brief or requirement document, **start with a concise summary** of what this skill expects and what it will generate, then ask for their requirement document before creating or editing anything in Figma:

1. **Explain What You Will Generate**:
   - Export-ready website sidebar ad banners built directly in **Figma** as editable auto-layout frames with exact fixed dimensions (`clipsContent` enabled):
     - **Half Page (`300×600` px)** — full vertical unit with brand lockup, headline, subheadline, visual metric/proof card, CTA button, and trust microcopy.
     - **Medium Rectangle (`300×250` px)** — compact universal sidebar unit with brand lockup, badge, headline, short subheadline, and CTA button.
     - **Wide Skyscraper (`160×600` px)** — narrow vertical sidebar unit with centered lockup, badge, headline, metric highlight, and CTA button.
2. **Explain the Expected Input Format**:
   - Accept a **requirement document** (pasted text, Markdown, or file) or the **structured brief** below. Clarify that headlines should be short (≤ 6 words), colors should be hex codes (or a brand theme), and any existing Figma file URL is optional (a new file will be created if omitted).
3. **Prompt with the Template**:

```markdown
### Sidebar Ad Banner Requirement Brief
- **Brand Name**: <Your Company / Product>
- **Logo / Visuals**: <Figma node/file link, image description, or "simple geometric mark">
- **Brand Colors**:
  - Background: <#HEX> (and optional secondary gradient <#HEX>)
  - Accent / CTA Button: <#HEX>
  - Text Primary / Muted: <#HEX> / <#HEX>
- **Font Family**: <e.g., Plus Jakarta Sans, Inter, DM Sans>
- **Campaign Copy**:
  - Badge (optional): <e.g., FREE TRIAL, 25% OFF, AD>
  - Headline (≤ 6 words): <Short punchy headline>
  - Subheadline (1 sentence): <Value proposition>
  - Metric / Proof Card (for tall banners): <e.g., +148% Campaign Lift>
  - CTA Copy: <e.g., Start Free Trial →, Shop Now →>
  - Trust Microcopy (optional): <e.g., No card required>
- **Target Sidebar Sizes**: <300×600 Half Page, 300×250 Medium Rectangle, 160×600 Wide Skyscraper>
- **Figma Destination**: <Existing Figma file URL or "Create new file">
```

*(If the user asks to test or preview with sample data, use a profile from [references/sample-campaigns.json](references/sample-campaigns.json) instead.)*

## Step 2: Figma Execution Workflow

1. **Prerequisites**:
   - Load `figma-use` and `figma-generate-design` skills before any mutating `use_figma` call.
   - If creating a new file, load `figma-create-new-file`, call `whoami` to resolve `planKey`, then call `create_new_file` with `editorType: "design"`.
   - Call `create_session` with the `fileKey` and pass the returned `sessionId` to all subsequent Figma MCP calls.
2. **Build Each Banner Frame**:
   - Use `figma.createAutoLayout('VERTICAL', ...)` for the outer banner frame, then call `resize(width, height)` and set `layoutSizingHorizontal = 'FIXED'`, `layoutSizingVertical = 'FIXED'`, and `clipsContent = true`.
   - **Important**: `figma.createAutoLayout()` defaults to a white fill—explicitly set `fills: []` on all transparent inner auto-layout containers (`Top Bar`, `Brand Lockup`, `Header & Copy`, `CTA Footer`, etc.).
   - Load every font family/style with `await figma.loadFontAsync(...)` before setting `characters` or font properties.
   - Set `textAutoResize = 'HEIGHT'` and `layoutSizingHorizontal = 'FILL'` on wrapping text blocks after appending to their parent.
   - Add a subtle `1px` border (`rgba(255,255,255,0.12)` on dark themes or `rgba(0,0,0,0.08)` on light themes) so banners stay crisp against any website background.
3. **Verify Visually**:
   - Call `await banner.screenshot()` at the end of the `use_figma` script and inspect the rendered PNGs to confirm no clipped text, no overlapping elements, and strong CTA contrast.
