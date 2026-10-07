# Reusable Complianz Cookie Banner Styling Guide

This guide provides a portable starting point for styling a Complianz banner on almost any WordPress site. All brand colors are defined once at the top of the CSS, so adapting it to another website should require changing only the variables.

The design deliberately gives the primary action modest visual emphasis while keeping rejection visible, readable, and available in one click. Avoid making the reject action smaller, lower-contrast, or harder to reach; doing so can undermine valid consent.

## 1. Recommended Complianz settings

Open **Complianz → Cookie Banner → Edit active banner**. Exact labels can vary slightly between versions and translations.

| Setting | Recommended value |
|---|---|
| Position | Center |
| Animation | None, or a subtle fade |
| Banner width | 600 px |
| Checkbox style | Slider |
| Legal documents on banner | Enable only if the links are useful and correctly generated |
| Logo | None by default; add only a compact logo if it improves trust without increasing mobile height |
| Close button | Off when Accept and Reject are both immediately available |
| Shadow | On |
| Header/footer internal shadow | Off |
| Soft cookie wall | Off |
| Banner corner radius | 16 px |
| Banner border width | 1 px |
| Button corner radius | 9–10 px |
| Base font size | 16 px |

If the close button is enabled, verify that closing the banner does not count as consent.

## 2. Recommended first-layer content

Use a short, visible heading that explains the decision:

> **Choose how we use cookies**

Describe the actual purposes and important providers in two or three sentences. A transferable template is:

> With your permission, we use optional cookies to understand which pages are useful and to measure the effectiveness of our campaigns. Some information is processed by [analytics providers] and [advertising providers]. The website’s essential features work if you decline, and you can change your choice at any time.

Recommended button labels:

- **Accept all**
- **Reject optional cookies**
- **Choose preferences**

Translate these naturally for the site’s language. Avoid vague labels such as “OK,” “Continue,” or “Got it.”

### Preventing awkward hyphenation

For languages that use a hyphenated word in the title, replace the ordinary hyphen (`-`) with a non-breaking hyphen (`‑`) when an undesirable mobile line break occurs. For example:

```text
cookie‑urile
```

## 3. Portable CSS

Paste the following into the active Complianz banner’s **Custom CSS** field. To transfer it to another site, change the variables in the first section and leave the component rules unchanged.

```css
/* =========================================================
   COMPLIANZ PORTABLE THEME

   Change the variables in this section when moving the
   banner to another website.
   ========================================================= */

:root {
    /* Brand palette */
    --cmplz-theme-primary: #007a3d;
    --cmplz-theme-primary-hover: #006332;
    --cmplz-theme-primary-text: #ffffff;
    --cmplz-theme-accent: #f5a623;

    /* Banner palette */
    --cmplz-theme-surface: #ffffff;
    --cmplz-theme-heading: #1f2933;
    --cmplz-theme-text: #4b5563;
    --cmplz-theme-border: #dde4e8;
    --cmplz-theme-link: #006b37;
    --cmplz-theme-link-hover: #004f2a;

    /* Secondary action palette */
    --cmplz-theme-secondary-surface: #f3f6f8;
    --cmplz-theme-secondary-hover: #e9eef2;
    --cmplz-theme-secondary-border: #d7e0e5;
    --cmplz-theme-secondary-border-hover: #bdc9d0;
    --cmplz-theme-secondary-text: #334155;

    /* Toggle palette */
    --cmplz-theme-toggle-active: #007a3d;
    --cmplz-theme-toggle-inactive: #64748b;
    --cmplz-theme-toggle-dot: #ffffff;

    /* Overlay and shadow */
    --cmplz-theme-overlay: rgba(7, 20, 32, 0.30);
    --cmplz-theme-shadow:
        0 20px 50px rgba(15, 35, 50, 0.18),
        0 4px 12px rgba(15, 35, 50, 0.08);

    /* Dimensions */
    --cmplz-theme-width: 620px;
    --cmplz-theme-radius: 16px;
    --cmplz-theme-mobile-radius: 14px;
    --cmplz-theme-button-radius: 9px;
    --cmplz-theme-desktop-padding: 24px;
    --cmplz-theme-mobile-padding: 18px;
}


/* =========================================================
   OPTIONAL VISUAL BACKDROP

   This backdrop is visual only. pointer-events:none keeps it
   from becoming a hard cookie wall.
   ========================================================= */

#cmplz-cookiebanner-container:has(.cmplz-cookiebanner.cmplz-show)::before {
    content: "";
    position: fixed;
    inset: 0;
    background: var(--cmplz-theme-overlay);
    z-index: 2147483645;
    pointer-events: none;
}

#cmplz-cookiebanner-container .cmplz-cookiebanner {
    z-index: 2147483646 !important;
}


/* =========================================================
   MAIN BANNER
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-cookiebanner {
    width: min(var(--cmplz-theme-width), calc(100vw - 32px)) !important;
    max-width: var(--cmplz-theme-width) !important;
    padding: var(--cmplz-theme-desktop-padding) !important;

    background: var(--cmplz-theme-surface) !important;
    color: var(--cmplz-theme-heading) !important;

    border: 1px solid var(--cmplz-theme-border) !important;
    border-top: 4px solid var(--cmplz-theme-accent) !important;
    border-radius: var(--cmplz-theme-radius) !important;
    box-shadow: var(--cmplz-theme-shadow) !important;
}


/* =========================================================
   HEADER AND TITLE
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-header {
    align-items: center !important;
    margin-bottom: 12px !important;
}

#cmplz-cookiebanner-container .cmplz-title {
    display: block !important;
    color: var(--cmplz-theme-heading) !important;
    font-size: 22px !important;
    font-weight: 700 !important;
    line-height: 1.25 !important;
    letter-spacing: -0.01em !important;
}

#cmplz-cookiebanner-container .cmplz-divider-header {
    display: none !important;
}


/* =========================================================
   DESCRIPTION
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-message {
    color: var(--cmplz-theme-text) !important;
    font-size: 15.5px !important;
    line-height: 1.55 !important;
}

#cmplz-cookiebanner-container .cmplz-message p {
    margin: 0 !important;
}


/* =========================================================
   BUTTON LAYOUT
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-buttons {
    display: grid !important;
    grid-template-columns: repeat(2, minmax(0, 1fr)) !important;
    gap: 10px !important;
    margin-top: 20px !important;
}

#cmplz-cookiebanner-container .cmplz-btn {
    min-height: 50px !important;
    padding: 11px 16px !important;
    border-radius: var(--cmplz-theme-button-radius) !important;
    font-size: 15px !important;
    font-weight: 650 !important;
    line-height: 1.25 !important;

    transition:
        background-color 160ms ease,
        border-color 160ms ease,
        box-shadow 160ms ease,
        transform 160ms ease !important;
}


/* Accept */

#cmplz-cookiebanner-container .cmplz-accept {
    background: var(--cmplz-theme-primary) !important;
    border: 2px solid var(--cmplz-theme-primary) !important;
    color: var(--cmplz-theme-primary-text) !important;
}

#cmplz-cookiebanner-container .cmplz-accept:hover {
    background: var(--cmplz-theme-primary-hover) !important;
    border-color: var(--cmplz-theme-primary-hover) !important;
    transform: translateY(-1px);
    box-shadow: 0 5px 12px color-mix(
        in srgb,
        var(--cmplz-theme-primary) 25%,
        transparent
    ) !important;
}


/* Reject — same size and strong visibility as Accept */

#cmplz-cookiebanner-container .cmplz-deny {
    background: var(--cmplz-theme-surface) !important;
    border: 2px solid var(--cmplz-theme-primary) !important;
    color: var(--cmplz-theme-link) !important;
}

#cmplz-cookiebanner-container .cmplz-deny:hover {
    background: color-mix(
        in srgb,
        var(--cmplz-theme-primary) 8%,
        var(--cmplz-theme-surface)
    ) !important;
    border-color: var(--cmplz-theme-primary-hover) !important;
}


/* Preferences and Save */

#cmplz-cookiebanner-container .cmplz-view-preferences,
#cmplz-cookiebanner-container .cmplz-save-preferences {
    grid-column: 1 / -1 !important;
    min-height: 44px !important;
    background: var(--cmplz-theme-secondary-surface) !important;
    border: 1px solid var(--cmplz-theme-secondary-border) !important;
    color: var(--cmplz-theme-secondary-text) !important;
}

#cmplz-cookiebanner-container .cmplz-view-preferences:hover,
#cmplz-cookiebanner-container .cmplz-save-preferences:hover {
    background: var(--cmplz-theme-secondary-hover) !important;
    border-color: var(--cmplz-theme-secondary-border-hover) !important;
}


/* =========================================================
   LEGAL DOCUMENT LINKS
   ========================================================= */

/* Separation between the preferences button and documents */

#cmplz-cookiebanner-container .cmplz-documents.cmplz-links {
    margin-top: 16px !important;
}

/* One legal document per row */

#cmplz-cookiebanner-container .cmplz-documents.cmplz-links ul {
    display: flex !important;
    flex-direction: column !important;
    align-items: stretch !important;
    gap: 7px !important;

    width: 100% !important;
    margin: 0 !important;
    padding: 0 !important;
    list-style: none !important;
}

#cmplz-cookiebanner-container .cmplz-documents.cmplz-links li {
    display: block !important;
    width: 100% !important;
    margin: 0 !important;
    padding: 0 !important;
}

#cmplz-cookiebanner-container .cmplz-documents.cmplz-links a {
    display: block !important;
    width: 100% !important;
    padding: 2px 0 !important;

    color: var(--cmplz-theme-link) !important;
    font-size: 14px !important;
    line-height: 1.35 !important;
    text-align: center !important;
    text-decoration: underline !important;
    text-underline-offset: 3px !important;
}

#cmplz-cookiebanner-container .cmplz-documents.cmplz-links a:hover {
    color: var(--cmplz-theme-link-hover) !important;
    text-decoration-thickness: 2px !important;
}


/* =========================================================
   TOGGLES
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-label::before {
    background-color: var(--cmplz-theme-toggle-inactive) !important;
}

#cmplz-cookiebanner-container .cmplz-consent-checkbox:checked + .cmplz-label::before {
    background-color: var(--cmplz-theme-toggle-active) !important;
}

#cmplz-cookiebanner-container .cmplz-label::after {
    background-color: var(--cmplz-theme-toggle-dot) !important;
}


/* =========================================================
   CLOSE BUTTON
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-close {
    color: var(--cmplz-theme-text) !important;
    opacity: 0.85;
}

#cmplz-cookiebanner-container .cmplz-close:hover {
    color: var(--cmplz-theme-heading) !important;
    opacity: 1;
}


/* =========================================================
   KEYBOARD ACCESSIBILITY
   ========================================================= */

#cmplz-cookiebanner-container .cmplz-btn:focus-visible,
#cmplz-cookiebanner-container .cmplz-close:focus-visible,
#cmplz-cookiebanner-container a:focus-visible {
    outline: 3px solid var(--cmplz-theme-accent) !important;
    outline-offset: 3px !important;
}


/* =========================================================
   MOBILE
   ========================================================= */

@media (max-width: 600px) {
    #cmplz-cookiebanner-container .cmplz-cookiebanner {
        width: calc(100vw - 20px) !important;
        padding: var(--cmplz-theme-mobile-padding) !important;
        border-radius: var(--cmplz-theme-mobile-radius) !important;
    }

    #cmplz-cookiebanner-container .cmplz-header {
        margin-bottom: 12px !important;
    }

    #cmplz-cookiebanner-container .cmplz-title {
        width: 100% !important;
        padding-right: 0 !important;

        font-size: 20px !important;
        line-height: 1.25 !important;
        letter-spacing: -0.01em !important;
        text-align: center !important;
    }

    #cmplz-cookiebanner-container .cmplz-message {
        font-size: 14.5px !important;
        line-height: 1.5 !important;
    }

    #cmplz-cookiebanner-container .cmplz-buttons {
        grid-template-columns: 1fr !important;
        gap: 9px !important;
        margin-top: 16px !important;
    }

    #cmplz-cookiebanner-container .cmplz-view-preferences,
    #cmplz-cookiebanner-container .cmplz-save-preferences {
        grid-column: auto !important;
    }

    #cmplz-cookiebanner-container .cmplz-documents.cmplz-links {
        margin-top: 14px !important;
    }

    #cmplz-cookiebanner-container .cmplz-documents.cmplz-links ul {
        gap: 8px !important;
    }
}


/* Very narrow phones */

@media (max-width: 350px) {
    #cmplz-cookiebanner-container .cmplz-cookiebanner {
        padding: 16px !important;
    }

    #cmplz-cookiebanner-container .cmplz-title {
        font-size: 18px !important;
    }

    #cmplz-cookiebanner-container .cmplz-message {
        font-size: 14px !important;
    }

    #cmplz-cookiebanner-container .cmplz-btn {
        padding-right: 10px !important;
        padding-left: 10px !important;
        font-size: 14px !important;
    }
}


/* =========================================================
   REDUCED MOTION
   ========================================================= */

@media (prefers-reduced-motion: reduce) {
    #cmplz-cookiebanner-container .cmplz-btn {
        transition: none !important;
    }

    #cmplz-cookiebanner-container .cmplz-accept:hover {
        transform: none !important;
    }
}
```

### Compatibility note

The optional backdrop uses the modern CSS `:has()` selector. It works in current versions of Chrome, Edge, Firefox, and Safari. If support for older browsers is important, remove the entire **Optional visual backdrop** section; the banner will continue to work normally.

The stylesheet also uses `color-mix()` for hover colors. For maximum legacy-browser compatibility, replace those two declarations with fixed colors appropriate to the selected palette.

## 4. Moving the design to another website

1. Copy the entire stylesheet into the other site’s active Complianz banner.
2. Replace the values under `:root` with that site’s brand colors.
3. Verify that white text on `--cmplz-theme-primary` has at least a 4.5:1 contrast ratio.
4. Verify that `--cmplz-theme-link` has at least a 4.5:1 contrast ratio against `--cmplz-theme-surface`.
5. Update the banner title, message, button labels, and provider names.
6. Remove unused consent categories in the Complianz wizard.
7. Clear the site, CDN, optimization, and generated CSS caches.
8. Test in a new private/incognito browser session.

## 5. Validation checklist

### Desktop

- The entire message and all three actions are visible without scrolling.
- Accept and Reject have the same dimensions and font weight.
- The banner does not cover an essential navigation or form control.
- Legal links appear on separate rows and lead to the correct documents.

### Mobile

- Test at 390 px, 360 px, and 320 px widths.
- The title does not split immediately after a hyphen.
- Each action occupies the full available width.
- No text or focus outline is clipped by the banner.
- The complete banner remains usable on a short viewport; internal scrolling is acceptable only when preference categories are expanded.

### Consent behavior

- No non-essential cookie or tag receives consent before a decision.
- Reject is available on the first layer and requires no more effort than Accept.
- Closing or ignoring the banner does not count as acceptance.
- The saved choice persists for the configured period.
- A permanent “Cookie settings” link allows the visitor to change or withdraw consent.
- Google, Meta, Hotjar, and other tags respond to the correct Complianz consent categories.

## 6. Measuring improvements

Do not evaluate the design using acceptance rate alone. Track:

- acceptance rate among visitors who make a choice;
- rejection rate;
- no-decision or dismissal rate;
- mobile bounce rate;
- lead or purchase conversion rate;
- banner interaction time;
- preference-layer usage.

When A/B testing, change one meaningful variable at a time—such as message length, title, or position—while keeping Accept and Reject equally accessible. This produces interpretable results and avoids optimizing for consent obtained through confusion.

