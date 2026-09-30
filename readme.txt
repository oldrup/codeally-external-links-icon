=== Codeally External Links Icon ===
Contributors: oldrup
Tags: external links, rel external, link icon, block editor, accessibility
Requires at least: 6.9
Tested up to: 7.1
Requires PHP: 8.2
Stable tag: 0.3.3
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Automatically appends rel="external" to external links and renders a link icon using pure CSS masks.

== Description ==

Codeally External Links Icon automatically detects external links in post content, appends `rel="external"` server-side, and renders an SVG external link icon using pure CSS masks[cite: 2].

Developed by [Bjarne Oldrup](https://oldrup.dk/) and sponsored by [Codeally](https://codeally.dk/)[cite: 2, 5].

== Frequently Asked Questions ==

=== Does this plugin have a settings page? ===
No. This plugin is intentionally zero-configuration with zero database options[cite: 2]. It works automatically upon activation by detecting external links in post content and rendering the icon server-side[cite: 2]. Icon customization is handled natively through CSS custom properties or utility classes[cite: 2, 3].

=== How do I customize icons globally or for a specific block? ===
You can switch between built-in presets globally or per block[cite: 2]:

- **Default Box Icon:** `--cdly-mask-image-box`[cite: 2]
- **Diagonal Arrow Icon:** `--cdly-mask-image-arrow`[cite: 2]

**Option 1 (No Code):** Select any block in the Block Editor and add `has-cdly-icon-arrow` under **Additional CSS Class(es)**[cite: 3]. All external links within that block will render with the diagonal arrow icon[cite: 3].

**Option 2 (CSS Property API):** Set `--cdly-external-links-icon: var(--cdly-mask-image-arrow);` in your theme stylesheet, Customizer, or Block Editor Custom CSS[cite: 2, 3].

=== What are the compatibility and browser baseline requirements? ===
- **Content Scope:** Built and tested strictly for native WordPress Core Block Editor content (Paragraphs, Buttons, Lists, etc.)[cite: 2]. Third-party page builders (Elementor, Bricks, Divi) are not officially supported[cite: 2].
- **Browser Baseline:** Uses CSS `:has()` pseudo-class targeting to prevent icons from rendering inside links that wrap images or inline SVGs[cite: 2]. Requires modern browsers supporting `:has()` and CSS alt-text (Chrome 105+, Safari 15.4+, Firefox 128+, Edge 105+)[cite: 2].

=== How does accessibility and internationalization (i18n) work? ===
- **Screen Reader Announced:** Uses CSS `content` alternative text syntax (`/ " (external link)"`) so screen readers (NVDA, JAWS, VoiceOver) announce external links naturally without cluttering the DOM with extra HTML `<span>` tags[cite: 2].
- **Fully Translatable:** All user-facing strings and screen reader labels use standard WordPress i18n functions (`__()`) and support custom translations via `.po` / `.mo` files in the `/languages/` folder[cite: 2].
- **High Contrast / WCAG Compliant:** Includes `@media (forced-colors: active)` fallbacks for Windows High Contrast mode (WCAG 1.4.11)[cite: 2].

=== What are the technical, database, and caching specifications? ===
- **Zero Database Footprint:** Makes no permanent modifications to post content or the database[cite: 2]. Disabling or removing the plugin leaves zero residual data or markup changes[cite: 2].
- **Page Cache Integration:** Injects `rel="external"` on `the_content` filter before page caching layers (WP Rocket, LiteSpeed, Redis, NGINX FastCGI) capture HTML output[cite: 2]. Cached page requests serve the rendered link markup with zero PHP overhead[cite: 2].
- **Streaming HTML Parser:** Uses WordPress core `WP_HTML_Tag_Processor` for sub-millisecond execution without creating full DOM trees or memory allocations[cite: 2].
- **Zero Client-Side JavaScript:** Renders icons strictly through browser-native CSS pseudo-elements and data-URI SVG masks without DOM mutations[cite: 2].
- **Zero-Specificity API:** Exposes `--cdly-external-links-icon` via `:where(:root)`, allowing theme stylesheets or block CSS to switch icon presets without specificity conflicts[cite: 2, 3].

== Screenshots ==

1. Front-end post content showing external links automatically decorated with the CSS mask icon[cite: 2].

== Installation ==

1. Upload the `codeally-external-links-icon` directory to `/wp-content/plugins/`[cite: 2].
2. Activate the plugin via the 'Plugins' menu in WordPress[cite: 2].
3. External links in post content will automatically receive `rel="external"` and the link icon on the front end[cite: 2].

== Changelog ==

= 0.3.3 =
- Added .has-cdly-icon-arrow utility class for toggling arrow icon presets via Block Editor CSS classes[cite: 3].
- Standardized CSS Custom Property naming (--cdly-external-links-icon) across stylesheet and documentation[cite: 2, 3].
- Verified compatibility with WordPress 7.1[cite: 2].

= 0.3.2 =
- Added --cdly-external-links-margin property to finetune margin between link and icon[cite: 2].

= 0.3.1 =
- Updated inline CSS string escaping to addslashes() and wp_strip_all_tags() for localized accessibility labels[cite: 2].
- Added License URI to main PHP header for full metadata parity across plugin files[cite: 2].
- Version bump and stable tag alignment[cite: 2].

= 0.3.0 =
- Added [target="_blank"] and [data-type="link"] to candidates for external links[cite: 2].
- Changed plugin slug to codeally-external-links-icon and updated related files and documentation[cite: 2].

= 0.2.0 =
- Introduced zero-specificity CSS Custom Property API (`--codeally-external-links-icon`) using `:where(:root)`[cite: 2].
- Added `--cdly-mask-image-arrow` (diagonal arrow) preset alongside `--cdly-mask-image-box` (default box icon)[cite: 2].
- Added support for container and block-level icon scoping in Block Editor Custom CSS[cite: 2].

= 0.0.10 =
- Removed redundant `load_plugin_textdomain()` call to support WordPress 4.6+ JIT translations without Plugin Check PCP warnings[cite: 2].

= 0.0.9 =
- Added text domain loading (`Domain Path: /languages`) for i18n translation support[cite: 2].
- Dynamic localized screen reader label injection via `wp_add_inline_style()`[cite: 2].

= 0.0.8 =
- Added screen reader accessibility context directly in CSS `content` syntax[cite: 2].
- Added `forced-colors: active` high-contrast mode media query for WCAG 1.4.11 compliance[cite: 2].
- Precision-tuned `:not(:has(svg, img))` selector and `margin-inline-start` punctuation handling[cite: 2].

= 0.0.7 =
- Updated short description syntax to pass Plugin Check PCP validation[cite: 2].

= 0.0.6 =
- Refactored front-end filtering lifecycle for maximum stability[cite: 2].

= 0.0.5 =
- Tested and optimized domain normalization logic[cite: 2].

= 0.0.4 =
- Improved PHP 8.2+ strict type handling on host comparison helpers[cite: 2].

= 0.0.3 =
- Replaced regex matching engine with WP_HTML_Tag_Processor for high-performance HTML stream parsing[cite: 2].
- Added www domain normalization[cite: 2].

= 0.0.1 =
- Initial standalone plugin release[cite: 2].