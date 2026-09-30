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

Codeally External Links Icon automatically detects external links in post content, appends `rel="external"` server-side, and renders an SVG external link icon using pure CSS masks.

Developed by [Bjarne Oldrup](https://oldrup.dk/) and sponsored by [Codeally](https://codeally.dk/).

== Frequently Asked Questions ==

=== What are the technical and performance specifications? ===
- **Zero Database Footprint:** Makes no permanent modifications to post content or the database.
- **Zero-Specificity Custom Property API:** Uses `:where(:root)` to expose `--cdly-external-links-icon`, allowing theme stylesheets or Block Editor custom CSS to switch icon presets without specificity conflicts.
- **Page Cache Integration:** Injects `rel="external"` on `the_content` filter before page caching layers (WP Rocket, LiteSpeed, Redis, NGINX FastCGI) capture HTML output.
- **Reversible:** Disabling or removing the plugin leaves zero residual data, orphan options, or markup changes in your database.
- **Streaming HTML Parser:** Uses WordPress core `WP_HTML_Tag_Processor` for sub-millisecond execution without creating full DOM trees or memory allocations.
- **Zero Client-Side JavaScript:** Renders icons strictly through browser-native CSS pseudo-elements and data-URI SVG masks without DOM mutations.

=== How do I customize icons via CSS or utility classes? ===
Switch between built-in presets globally or per-block:

- **Default Box Icon:** `--cdly-mask-image-box`
- **Diagonal Arrow Icon:** `--cdly-mask-image-arrow`

Set `--cdly-external-links-icon: var(--cdly-mask-image-arrow);` in your theme stylesheet, Customizer, or Block Editor Custom CSS.

Alternatively, add the helper class `has-cdly-icon-arrow` to any block's **Additional CSS Class(es)** setting.

=== How does accessibility and internationalization (i18n) work? ===
- **Screen Reader Announced:** Uses CSS `content` alternative text syntax (`/ " (external link)"`) so screen readers (NVDA, JAWS, VoiceOver) announce external links naturally without cluttering the DOM with extra HTML `<span>` tags.
- **Fully Translatable:** All user-facing strings and screen reader labels use standard WordPress i18n functions (`__()`) and support custom translations via `.po` / `.mo` files in the `/languages/` folder.
- **High Contrast / WCAG Compliant:** Includes `@media (forced-colors: active)` fallbacks for Windows High Contrast mode (WCAG 1.4.11).

=== What are the compatibility and browser baseline requirements? ===
- **Content Scope:** Built and tested strictly for native WordPress Core Block Editor content (Paragraphs, Buttons, Lists, etc.). Third-party page builders (Elementor, Bricks, Divi) are not officially supported.
- **Browser Baseline:** Uses CSS `:has()` pseudo-class targeting to prevent icons from rendering inside links that wrap images or inline SVGs. Requires modern browsers supporting `:has()` and CSS alt-text (Chrome 105+, Safari 15.4+, Firefox 128+, Edge 105+).

=== How do I change the external link icon for a specific block? ===
Select any block in the Block Editor, expand **Advanced** in the block settings sidebar, and add `has-cdly-icon-arrow` under **Additional CSS Class(es)**.

Alternatively, in block Custom CSS, set:
`--cdly-external-links-icon: var(--cdly-mask-image-arrow);`

=== Does this plugin edit my database or post content? ===
No. Modifications occur purely in memory during the execution of `the_content` filter. Original database content remains untouched.

=== How does this interact with page caching plugins? ===
Because `rel="external"` is injected server-side during the initial HTML request, page cache engines store the processed HTML string directly. Subsequent cached page requests serve the rendered link markup with zero PHP overhead.

=== Does this plugin have a settings page? ===
No. This plugin is intentionally zero-configuration with zero database options. Icon customization is handled natively through CSS custom properties.

== Screenshots ==

1. Front-end post content showing external links automatically decorated with the CSS mask icon.

== Installation ==

1. Upload the `codeally-external-links-icon` directory to `/wp-content/plugins/`.
2. Activate the plugin via the 'Plugins' menu in WordPress.
3. External links in post content will automatically receive `rel="external"` and the link icon on the front end.

== Changelog ==

= 0.3.3 =
- Added .has-cdly-icon-arrow utility class for toggling arrow icon presets via Block Editor CSS classes.
- Standardized CSS Custom Property naming (--cdly-external-links-icon) across stylesheet and documentation.
- Verified compatibility with WordPress 7.1.

= 0.3.2 =
- Added --cdly-external-links-margin property to finetune margin between link and icon.

= 0.3.1 =
- Updated inline CSS string escaping to addslashes() and wp_strip_all_tags() for localized accessibility labels.
- Added License URI to main PHP header for full metadata parity across plugin files.
- Version bump and stable tag alignment.

= 0.3.0 =
- Added [target="_blank"] and [data-type="link"] to candidates for external links.
- Changed plugin slug to codeally-external-links-icon and updated related files and documentation.

= 0.2.0 =
- Introduced zero-specificity CSS Custom Property API (`--codeally-external-links-icon`) using `:where(:root)`.
- Added `--cdly-mask-image-arrow` (diagonal arrow) preset alongside `--cdly-mask-image-box` (default box icon).
- Added support for container and block-level icon scoping in Block Editor Custom CSS.

= 0.0.10 =
- Removed redundant `load_plugin_textdomain()` call to support WordPress 4.6+ JIT translations without Plugin Check PCP warnings.

= 0.0.9 =
- Added text domain loading (`Domain Path: /languages`) for i18n translation support.
- Dynamic localized screen reader label injection via `wp_add_inline_style()`.

= 0.0.8 =
- Added screen reader accessibility context directly in CSS `content` syntax.
- Added `forced-colors: active` high-contrast mode media query for WCAG 1.4.11 compliance.
- Precision-tuned `:not(:has(svg, img))` selector and `margin-inline-start` punctuation handling.

= 0.0.7 =
- Updated short description syntax to pass Plugin Check PCP validation.

= 0.0.6 =
- Refactored front-end filtering lifecycle for maximum stability.

= 0.0.5 =
- Tested and optimized domain normalization logic.

= 0.0.4 =
- Improved PHP 8.2+ strict type handling on host comparison helpers.

= 0.0.3 =
- Replaced regex matching engine with WP_HTML_Tag_Processor for high-performance HTML stream parsing.
- Added www domain normalization.

= 0.0.1 =
- Initial standalone plugin release.