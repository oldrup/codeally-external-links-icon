=== Codeally External Links Icon ===
Contributors: oldrup
Tags: external links, rel external, link icon, block editor, accessibility
Requires at least: 6.9
Tested up to: 7.1
Requires PHP: 8.2
Stable tag: 0.4.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Automatically appends rel="external" to external links and renders a link icon using pure CSS masks.

== Description ==

Codeally External Links Icon automatically detects external links in post content, appends `rel="external"` server-side, and renders an SVG external link icon using pure CSS masks.

Developed by [Bjarne Oldrup](https://oldrup.dk/) and sponsored by [Codeally](https://codeally.dk/).

== Frequently Asked Questions ==

=== Does this plugin have a settings page? ===
No. This plugin is intentionally zero-configuration with zero database options. It works automatically upon activation by detecting external links in post content, adding `rel="external"` during content rendering, and rendering the icon with CSS. Icon customization is handled natively through CSS custom properties or utility classes.

=== What happens to links that open in a new tab or window? ===
The stylesheet displays an icon on links with `target="_blank"`, including navigation buttons that open in a new tab or window. These links receive only a visual indicator; the PHP filter does not add `rel="external"` or the localized screen-reader label. If needed, use the accessibility options provided by your theme or page builder to describe this behavior. Opening links in new tabs should be used sparingly.

=== How do I customize icons globally or for a specific block? ===
You can switch between built-in presets globally or per block:

- **Default Box Icon:** `--cdly-mask-image-box`
- **Diagonal Arrow Icon:** `--cdly-mask-image-arrow`

**Option 1 (No Code):** Select any block in the Block Editor and add `has-cdly-icon-arrow` under **Additional CSS Class(es)**. All external links within that block will render with the diagonal arrow icon.

**Option 2 (CSS Property API):** Set `--cdly-external-links-icon: var(--cdly-mask-image-arrow);` in your theme stylesheet, Customizer, or Block Editor Custom CSS.

=== What are the compatibility and browser baseline requirements? ===
- **Content Scope:** Built and tested strictly for native WordPress Core Block Editor content (Paragraphs, Buttons, Lists, etc.). Third-party page builders (Elementor, Bricks, Divi) are not officially supported.
- **Theme Testing:** Tested with the latest available versions of Twenty Twenty-Five, Greyd, and Ollie (Full Site Editing themes), and Blocksy, Kadence, and GeneratePress (classic themes), as of September 2026.
- **Browser Support:** Designed for modern versions of Chrome, Safari, and Firefox. Uses modern CSS features such as `:has()`. Browsers released in 2023 or later should generally support the required features.

=== How does accessibility and internationalization (i18n) work? ===
- **Screen Reader Label:** Adds a localized `external link` label through CSS alternative text where supported, without adding extra elements to the link markup.
- **Accessibility Testing:** Tested keyboard navigation and screen-reader output with NVDA and Windows 11 Narrator. Both announced the localized external-link label provided through CSS alternative text.
- **Translation Support:** The screen-reader label uses WordPress i18n functions and can be translated through `.po` and `.mo` files in the `/languages/` folder.

=== What are the technical, database, and caching specifications? ===
- **No Database Changes:** Does not create database tables or options, or permanently modify post content. The `rel="external"` attribute is added when content is rendered.
- **Page Cache Integration:** Injects `rel="external"` through the `the_content` filter during page generation. When a page cache stores the generated HTML, subsequent cached requests can serve the markup without running this PHP filter again.
- **HTML Parser:** Uses WordPress core `WP_HTML_Tag_Processor` to process links without constructing a full DOM tree.
- **No JavaScript Required:** Renders icons with CSS pseudo-elements and inline SVG masks without modifying the document with JavaScript.
- **Icon Customization:** Exposes `--cdly-external-links-icon` with zero specificity, allowing theme stylesheets or block CSS to override the default icon.

== Screenshots ==

1. screenshot-1.png

== Installation ==

1. Upload the `codeally-external-links-icon` directory to `/wp-content/plugins/`.
2. Activate the plugin via the 'Plugins' menu in WordPress.
3. External links in post content will automatically receive `rel="external"` and the link icon on the front end.

== Changelog ==

= 0.4.0 =
- Improved localized CSS alternative-text serialization with `wp_json_encode()`.
- Documented theme, browser, keyboard-navigation, and screen-reader testing.
- Documented the visual-only icon behavior for links that open in a new tab or window.
- Added a front-end screenshot.