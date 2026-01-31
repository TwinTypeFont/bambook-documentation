---
title: Terms & Typography Guide
order: 1
slug: tips
---

<style>
    p{
        text-align:start;
    }
</style>    



## CJK Typesetting: The Nitty-Gritty

This doc is your guide to mastering high-quality vertical text layout using the `Bambook` package.

### CJK Fonts & Glyph Variations
"CJK" is the tech world's shorthand for **Chinese, Japanese, and Korean**. Unicode groups most of their shared characters into the same blocks. But in reality, "Chinese" splits further into Traditional (Traditional Chinese) and Simplified (Simplified Chinese). And if you want to get specific, Traditional Chinese has its own flavors for Hong Kong and Taiwan.

Characters might *look* the same, but their "glyph shapes" vary by region. Take "Source Han Sans" (Noto Sans CJK) for example. The Traditional Chinese version follows Taiwan's Ministry of Education standard (Standard Form of National Characters), looking a bit more like Kai style. The Hong Kong version follows its own local conventions. The Simplified Chinese version sticks to China's GB-18030 standard. Japanese follows JIS, and Korean glyphs keep a more traditional "block-print" vibe.

![Regional Glyph Variations](assets/images/f879a8a3f3771c9801a064670b549b67.jpg)

Even within "Traditional Chinese Heiti (roughly equivalent to Latin sans-serif, but NOT THE SAME)," there are differences.

![Slight variations in Traditional Chinese fonts](assets/images/e3897b31a833ae2aa417ae94eaadac86.jpg)

This package focuses on **CJK punctuation and layout rules** (like punctuation positioning, general conventions, etc.). We don't mess with the actual font glyph shapes—that's the font's job.
{: .tips-info}


### UTR #50
UTR #50 stands for **Unicode Technical Report #50**. It's the bible for vertical text layout in Unicode, covering orientation and rules for Latin characters too. It defines three main orientation properties: U (Upright), R (Rotated 90° clockwise side-ways), Tu (Transformed Upright), and Tr (Transformed Rotated).

Bambook tries its best to stick to UTR #50 specs, so you don't have to worry about the deep magic.
{: .tips-info}

### ISO 639-1
ISO 639-1 is the international standard for two-letter language codes (Alpha-2). We use these to label languages, often paired with BCP 47 (like `zh-TW`).

### W3C
The World Wide Web Consortium. They define the web standards we live by (HTML, CSS).

Bambook's syntax often takes inspiration from CSS declarations. Because why reinvent the wheel?
{: .tips-info}

<hr>

## CJK Layout Principles & Bambook Pro-Tips
This chapter covers the basics of vertical CJK typesetting. Actual usage might vary based on region or personal style. Think of these as "pirate guidelines" rather than strict laws—adjust as needed!


### Direction of Text, (Flow)

In vertical layout for Chinese, Japanese, and Korean, text almost always flows **Top-to-Bottom, Right-to-Left**. Traditional Mongolian, on the other hand, flows Left-to-Right.

![各語系間，標點符號位置差異](assets/images/1ff52e336e1bf01241eb10f76dc0c669.jpg)

### Vertical Text Alignment
`Bambook` gives you 4 strategies to align your text columns:

1. **Top** (Block A): Pins text to the top edge. Default behavior.
2. **Center** (Block B): Floats text in the vertical center.
3. **Bottom** (Block C): Anchors text to the bottom edge.
4. **Justify** (Block D): Distributed alignment. It automatically adjusts character spacing so the column hits both top and bottom edges perfectly.

![Text Alignment Diagram](assets/images/7a88f18ed4f685b50aeffa39b8542fc0.jpg)

### Punctuation in Vertical Layouts
Generally, Traditional Chinese places punctuation in the **center** of the vertical line. Simplified Chinese and Japanese place it in the **top-right** corner of the character box. (Korean rarely uses vertical mixed script nowadays, so we'll skip that).

For the best results, make sure you set `BambookLanguage` correctly **AND** use a matching font. If you're designing a Traditional Chinese interface but using a Simplified Chinese or Japanese font (or vice versa), your punctuation might look wonky even with the correct language setting.

![Punctuation differences](assets/images/60bd3660d7c06709bdd01d96263ab584.jpg)

On some Android versions, the default system font might load the correct Chinese characters but still use Simplified Chinese punctuation shapes/positions. In this case, we recommend enabling `punctuationFixMode`.
{: .tips-tip}

### Handling Latin & Digits in Vertical Text
Normally, we handle Latin characters and digits in two main ways:
1.  **Vertical `.mixed`**: (See Block A) Characters are rotated 90 degrees clockwise (standing sideways).
2.  **Upright `.upright`**: (See Block B) Characters stand upright, stacked vertically.
(This corresponds to the U and R property values in UTR #50).

`BambookTextOrientation` also provides a third mode: `tateChuYoko`. This forces **ALL** Latin/European text to be displayed horizontally. (See Block C). **Caution:** This affects *everything*, regardless of length, so use it wisely!

In Japanese typography, you often see short strings (2 digits or letters) kept horizontal, like "US", "25", "OK". Bambook supports this via the `tateChuYoko(bool, int)?` parameter.
Set it to `true` and define the max character count (inclusive).
For example, `orientation: BambookTextOrientation.mixed` combined with `tateChuYoko: (true, 2)` means:
- Normal Latin text is rotated (sideways).
- But any string with <= 2 characters (like "UI" in Block D) will be treated as Tate-chu-yoko (horizontal-in-vertical).

![Latin text handling examples](assets/images/8323bc28f3999563112393ecd0cd8993.jpg)

Heads up! `tateChuYoko` currently doesn't support advanced GSUB features, so it might not be perfect. Use your judgment.
{: .tips-info}

For the character count in `tateChuYoko`: Passing a negative integer disables it. Theoretically, in Dart, you could pass up to 2^63-1 (or whatever ECMAScript allows on Web), but... please don't. If you want *lots* of horizontal Latin text, just use `BambookTextOrientation.tateChuYoko`.
{: .tips-warning}


### Kinsoku (Line Breaking Rules)
"Kinsoku" (Japanese for "prohibition rules") ensures punctuation marks don't end up in awkward places—like a period starting a new line. It keeps the text looking clean. Usually, "points" like commas, periods, and colons cannot start a line.
This is enabled by default. You can control it via `applyKinsoku: bool`. If you're not writing in CJK or have a special use case, feel free to turn it off.

![Kinsoku text wrapping](assets/images/c419be0729b5173eadb0183b50500df0.jpg)


In Bambook 0.0.4, Kinsoku uses a "push-out" logic. We're working on smarter, more flexible algorithms for future versions.
{: .tips-info}

### Line Height & Character Spacing

In default Flutter `Text`, you use `height` and `letterSpacing`. Bambook uses these under the hood, but exposes its own controls: `lineSpacing` and `letterSpacing`.
Default `height` *technically* still works, but we recommend sticking to Bambook's parameters to avoid confusion and side effects.

---
Hope this guide levels up your Bambook game xd! enjoy!
