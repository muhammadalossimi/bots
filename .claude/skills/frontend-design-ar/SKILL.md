---
name: frontend-design-ar
description: Distinctive, intentional visual design for web UI with first-class Arabic and RTL support — landing pages, bot dashboards, chat interfaces, admin panels, components. Use this skill whenever building a new page, screen or component, or restyling/redesigning an existing one, and especially when the interface is in Arabic, bilingual Arabic/English, right-to-left, or for a bot (Telegram, Discord, WhatsApp, AI chat) — even if the user only says "make a page", "صمم واجهة", "اعمل لوحة تحكم" or "خلّيها أحلى" without mentioning design or RTL. Takes precedence over the generic frontend-design skill for Arabic or bilingual work.
license: Apache-2.0. Derived from Anthropic's frontend-design skill; complete terms in LICENSE.txt
---

# Frontend Design (Arabic-first)

Approach this as the design lead at a studio known for giving every client a distinct visual identity. The client has rejected proposals that felt templated and is paying for a point of view: make deliberate choices about palette, typography and layout that are specific to this brief, and take aesthetic risk when it's justified.

This version adds three things to that stance: Arabic and right-to-left interfaces are treated as a first-class target (not a mirrored afterthought), the stack follows whatever the project already uses, and there's specific guidance for bot dashboards and chat UIs.

## 0. Before designing: read the context

1. **Stack.** Look at the project first. If it already uses React, Next.js, Vue, Tailwind, a component library or a CSS methodology, build in that — a beautiful page in the wrong stack is a rewrite. With no project (or an empty one), produce a single self-contained `index.html` with inline CSS and only the JS it needs.
2. **Language and direction.** Decide which of these the brief is:
   - **Arabic** → `<html lang="ar" dir="rtl">`.
   - **English** → `lang="en" dir="ltr"`.
   - **Bilingual** → pick the primary language for `<html>`, and mark every block in the other language with its own `lang` + `dir`. If the user can switch language, the switch flips `dir` on `<html>` and the layout must hold in both.
   - When the brief is written in Arabic and says nothing about language, the interface is Arabic.
3. **Subject.** If the brief doesn't name what the product is, who it's for and the page's main job, propose one concrete answer yourself and state it. The subject's world — its materials, vernacular, the culture of its users — is where distinctive choices come from. A Gulf real-estate bot and a Moroccan recipe bot should not look alike.

## 1. RTL done right

RTL is not `direction: rtl` on the body and done. The reason to be careful: a half-mirrored interface (text flows right, but arrows, padding and progress bars still point left) reads as broken to native readers immediately.

- **Use logical CSS properties everywhere**: `margin-inline-start/end`, `padding-inline`, `inset-inline-start`, `border-inline-start`, `text-align: start/end`. Avoid `left`/`right` and `margin-left`/`padding-right` entirely, so the same stylesheet works in both directions. In Tailwind use `ms-*`, `me-*`, `ps-*`, `pe-*`, `start-*`, `end-*`, `text-start`, and `rtl:`/`ltr:` variants only for genuine exceptions.
- **Flexbox and grid already follow `dir`**; don't fight them with `row-reverse`.
- **Mirror directional icons** (back/forward arrows, chevrons, "send" icons, progress direction, sliders): `[dir="rtl"] .icon-directional { transform: scaleX(-1); }`. **Don't mirror** non-directional icons: checkmarks, play/pause (media controls stay LTR), clocks, logos, search magnifier, phone.
- **Keep LTR islands LTR**: code, URLs, emails, phone numbers, file paths, version numbers, and English brand names inside Arabic text. Wrap them in `<bdi>` or `<span dir="ltr">` so punctuation doesn't jump to the wrong side. Inputs for email/URL/phone get `dir="ltr"`.
- **Numerals**: choose deliberately between Western digits (0-9, the norm in most tech UIs and the Maghreb) and Eastern Arabic digits (٠-٩, common in Gulf/Levant editorial contexts). Be consistent within one interface. `Intl.NumberFormat('ar-EG')` gives Eastern digits; `'ar-u-nu-latn'` gives Western.
- **Charts and timelines**: time axes in an Arabic UI usually run right-to-left; say what you chose. Numeric axes stay as they are.
- Verify by actually rendering in RTL (screenshot if you can) and scanning for anything still pointing the wrong way.

## 2. Typography

Typography carries the personality of the page. Use one family or two, clearly distinct.

**Arabic type has rules Latin type doesn't** — breaking them makes text look broken, not stylish:
- **Never apply `letter-spacing` to Arabic text.** Arabic letters connect; spacing tears the joins apart. If a Latin heading style uses tracking, scope it with `:lang(en)` so it never hits Arabic.
- **No synthetic italic or all-caps.** Arabic has neither; `font-style: italic` produces an ugly slant. For emphasis use weight, size, color, or a contrasting family.
- **More line-height**: ~1.7–1.9 for Arabic body text (vs ~1.5 for Latin), because of tall ascenders and deep descenders and diacritics.
- **Arabic reads optically smaller** than Latin at the same `font-size`. In bilingual layouts bump Arabic ~10–15% or pick a pairing whose x-heights match.
- **Line length** under ~70 characters for Arabic body.
- **Kashida (tatweel) justification** is fine for editorial headlines, never for body text in a UI.

**Pick fonts deliberately.** `references/arabic-fonts.md` has a curated list with each typeface's personality, weights, and good Latin pairings. Read it before choosing type for any Arabic or bilingual interface. Don't reach for the same face every time — the default "Cairo/Tajawal for everything" is the Arabic equivalent of Inter-for-everything.

For Latin-only work, choose faces specific to the brief rather than the defaults you'd reach for on any project, and set a clear type scale.

Avoid these generated-page tells: accenting a single word in a headline with a different color/italic; all-caps labels; unnecessary eyebrow labels above every heading.

## 3. Avoid the defaults

AI-generated design currently clusters around a few looks. All are legitimate for some briefs, but they appear regardless of subject, so they're defaults rather than choices:

1. warm cream background (~#F4F1EA) + high-contrast serif + terracotta accent (~#D97757 — Anthropic's own accent, so it reads as a tell);
2. near-black background with a single acid-green or vermilion accent;
3. broadsheet layout: hairline rules, zero radius, dense newspaper columns;
4. the SaaS card kit: identical rounded cards, one radius everywhere, the same soft grey shadow, gradient washes;
5. template chrome: tracked ALL-CAPS eyebrows, "A · B · C" meta strings, "WORD — fragment" labels, #0B0B0B standing in for black, monospace for small labels, "→" appended to every link;
6. **Arabic-specific clichés**: generic geometric "Islamic pattern" backgrounds, gold-on-dark-green, mosque silhouettes or crescents used as decoration when the subject has nothing to do with them. Use cultural motifs only when they come from the actual subject.

Where the brief pins down a direction, follow it exactly — the brief always wins, even when it asks for one of these. Where it leaves an axis free, don't spend that freedom on a default.

## 4. Process: plan → review → build → critique

**Pass 1 — plan.** Write a compact design plan before code:
- **Color**: 4–6 named hex values.
- **Type**: typefaces and their roles (Arabic and Latin if bilingual), sizes, line-heights.
- **Layout**: one-sentence concept plus a small ASCII wireframe. Draw it in the reading direction you're building (for RTL, the primary column/nav starts on the right). State alignment.
- **Principles**: what makes this one specific to the brief.

**Pass 2 — review the plan.** Ask: is any part of this what I'd produce for any similar page? If so, revise it and say what changed and why. Only then write code.

**Build.** Watch CSS specificity — type selectors and class selectors cancelling each other's padding between sections is a common bug.

**Critique.** Render it and look (screenshot if possible, in both directions if bilingual). Spend your boldness in one place: one memorable element, everything around it quiet. Before finishing, remove one accessory.

Meet a quality floor without announcing it: responsive down to 360px mobile, visible keyboard focus, `prefers-reduced-motion` respected, WCAG AA contrast, works in RTL and LTR as applicable.

## 5. Motion

Use non-user-triggered motion sparingly — one orchestrated moment (a page-load sequence or a single reveal) lands better than fade-up on every section. Motion that answers an action (opening, expanding, confirming, a message arriving) is welcome when it shows what changed. In RTL, horizontal slide-ins come from the inline-start side (the right), so use logical values or flip with `[dir="rtl"]`.

## 6. Bot dashboards and chat interfaces

These are tools people return to daily, so clarity beats spectacle. Put the distinctive moment in one place (the header, the empty state, the brand mark) and keep the working surface calm.

**Dashboards for bots** (Telegram/Discord/WhatsApp/AI bots):
- Lead with what an operator checks first: is the bot up, how many users/messages today, what's failing. Status should be readable at a glance — color plus a word or icon, never color alone.
- Show real-looking data with realistic variance (not 1,234 / 5,678), and Arabic names/content when the bot serves Arabic users.
- Tables of users/messages/logs: sticky header, numbers aligned to end, timestamps relative ("قبل ٣ دقائق") with the absolute time on hover, LTR islands for IDs and usernames.
- Settings for commands, tokens, webhooks: name things in the user's terms ("الرسالة الترحيبية", not `welcome_msg`). Mask secrets with a reveal/copy action.
- Avoid the SaaS card kit (default #4): vary density and hierarchy — not every metric deserves the same card.

**Chat interfaces:**
- In RTL, the user's own messages sit on the inline-end side (left) and the bot's on the inline-start side (right) — the mirror of LTR. Use logical alignment so this follows `dir` automatically.
- Bubble text inherits the message's own direction: use `dir="auto"` on each message so a mixed Arabic/English conversation lays out correctly per message.
- The composer: `dir="auto"` on the textarea, send button mirrored in RTL, Enter to send / Shift+Enter for newline, visible disabled state while sending.
- Design the states: empty conversation (suggest what to ask), typing indicator, streaming text, error with retry, long code blocks (LTR, horizontally scrollable).

## 7. Writing in the interface

Words exist to make the interface easier to understand and use.

- Write from the user's perspective, in plain language: "إدارة الإشعارات", not "إعدادات الـ webhook".
- Buttons say exactly what happens, and the name stays consistent through the flow: a "نشر" button produces a "تم النشر" toast.
- Errors explain what happened and how to fix it; they don't apologize and aren't vague. Empty states invite action.
- **Arabic register**: default to clear Modern Standard Arabic, light and direct — not stiff formal prose, not dialect, unless the brief asks for a dialect or the brand is clearly local (then commit to it consistently). Avoid literal translations of English UI idioms; write what an Arabic-speaking designer would write.
- Never use lorem ipsum or "نص تجريبي". Write real copy for the subject.
