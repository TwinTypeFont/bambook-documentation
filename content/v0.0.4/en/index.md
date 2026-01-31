---
title: Bambook-DOC_V0.0.4
order: 0
slug: index
---


# Bambook: An open-source vertical typesetting package for Flutter.

Vertical text is common across many East Asian weiting system(e.g.CJKV). But ironically, Flutter **does not** provide a native vertical text box. Bambook is here to save the day, allowing developers to quickly create vertical text layouts.

![Vertical Typesetting Possibilities](assets/images/003.jpg)

pub.dev link: <https://pub.dev/packages/bambook/>

## Getting Started

First, add `bambook` to your dependencies in `pubspec.yaml`:

```yaml
dependencies:
  bambook: ^0.0.4 # or newer
```

Next, import the package in your Dart code:

```dart
import 'package:bambook/bambook.dart';
```

## `BambookText` Syntax Overview

`BambookText` is the core Widget of this package. Its usage is very similar to Flutter's native `Text` Widget.

```dart
const BambookText(
  "Seasons change, sun and moon revolve, only the ink remains as solid as stone. --TwinType",
  style: TextStyle(
    fontSize: 22,
    color: Color.fromARGB(255, 8, 19, 76),
    fontFamily: 'LINESeed-TW_Rg',
  ),
  textAlign: BambookTextAlign.justify,
  language: BambookLanguage.tc,
  direction: BambookTextDirection.rtl,
  orientation: BambookTextOrientation.mixed,
  applyKinsoku: true,
  tateChuYoko: (false, 0), 
  punctuationFixMode: PunctuationFixMode.auto,
  lineSpacing: 24.0,
  letterSpacing: -10,
);

```

## Parameters Deep Dive

Here's the lowdown on every parameter in `BambookText`:

<div style="overflow-x:scroll;">
<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Type</th>
      <th>Default</th>
      <th style="text-align: left; min-width: 600px;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>data</code></td>
      <td><code>String</code></td>
      <td><strong>Required</strong></td>
      <td style="text-align: left">The text content you want to display.</td>
    </tr>
    <tr>
      <td><code>style</code></td>
      <td><code>TextStyle?</code></td>
      <td><code>null</code></td>
      <td style="text-align: left">Text style. Supports properties like <code>fontSize</code>, color, etc.</td>
    </tr>
    <tr>
      <td><code>textAlign</code></td>
      <td><code>BambookTextAlign</code></td>
      <td><code>BambookTextAlign.top</code></td>
      <td style="text-align: left">Sets the <strong>vertical alignment for a single line</strong>. Options: <code>top</code>, <code>center</code>, <code>bottom</code>, and <code>justify</code> (distributes text evenly).</td>
    </tr>
    <tr>
      <td><code>direction</code></td>
      <td><code>BambookTextDirection</code></td>
      <td><code>BambookTextDirection.rtl</code></td>
      <td style="text-align: left">Sets the <strong>line wrapping direction</strong>. Options: <code>rtl</code> (Right-to-Left, for traditional CJK), or <code>ltr</code> (Left-to-Right).</td>
    </tr>
    <tr>
      <td><code>orientation</code></td>
      <td><code>BambookTextOrientation</code></td>
      <td><code>BambookTextOrientation.mixed</code></td>
      <td style="text-align: left">Controls the <strong>orientation of Latin characters and digits</strong>. Three modes: <br>1. <code>mixed</code>: Rotates them 90° clockwise (sideways). <br>2. <code>upright</code>: Keeps them upright. <br>3. <code>tateChuYoko</code>: Forces them into horizontal orientation.</td>
    </tr>
    <tr>
      <td><code>language</code></td>
      <td><code>BambookLanguage</code></td>
      <td><code>BambookLanguage.tc</code></td>
      <td style="text-align: left">
<strong>Language Setting</strong>. This affects the <strong>default position of punctuation</strong>. <br><code>tc</code> (Trad. Chinese) centers punctuation. <br><code>sc</code> (Simp. Chinese), <code>jp</code> (Japanese), <code>kr</code> (Korean) align punctuation to the top-right (or corner). This aligns with regional typesetting standards.</td>
    </tr>
    <tr>
      <td><code>applyKinsoku</code></td>
      <td><code>bool</code></td>
      <td><code>true</code></td>
      <td style="text-align: left">Enables <strong>Kinsoku (Line breaking rules)</strong>. Prevents punctuation marks (like commas and periods) from appearing at the start of a line.</td>
    </tr>
    <tr>
      <td><code>lineSpacing</code></td>
      <td><code>double</code></td>
      <td><code>10.0</code></td>
      <td style="text-align: left">
<strong>Extra Line Spacing</strong>. Adds extra space (logic pixels) <strong>between columns/lines</strong>.<br><strong>WARNING:</strong> Do not use <code>text.style.height</code> or set it to <code>1</code>, as it's a default Flutter text parameter that can cause issues in Bambook.
</td>
    </tr>
    <tr>
      <td><code>letterSpacing</code></td>
      <td><code>double</code></td>
      <td><code>0.0</code></td>
      <td style="text-align: left">
<strong>Vertical Character Spacing</strong>. Sets extra vertical space between characters <strong>within the same line</strong>.<br><strong>WARNING:</strong> Do not use <code>style.letterSpacing</code> from `TextStyle`, as it increases <strong>horizontal width</strong> instead of vertical spacing. Use this parameter for vertical gap.</td>
    </tr>
    <tr>
      <td><code>punctuationFixMode</code></td>
      <td><code>PunctuationFixMode</code></td>
      <td><code>PunctuationFixMode.auto</code></td>
      <td style="text-align: left">
<strong>Punctuation Position Fix</strong>. Since OS fonts (especially on Android) vary in CJK support, punctuation might be off-center in vertical mode. <br>- <code>auto</code>: Based on font configuration.<br>- <code>force</code>: Force fix.<br>- <code>disable</code>: Disable fix. Recommended if using custom fonts (like <code>Noto Sans TC</code>) or on iOS/macOS for best performance.</td>
    </tr>
    <tr>
      <td><code>tateChuYoko</code></td>
      <td><code>(bool, int)?</code></td>
      <td><code>null</code></td>
      <td style="text-align: left">
<strong>Tate-chu-yoko (Horizontal-in-Vertical)</strong>. When set to <code>(bool, N)</code>, consecutive Latin/digits with length <strong><= N</strong> will be rotated to horizontal. <br>E.g., <code>tateChuYoko: (true, 2)</code> makes "A1" or "25" horizontal. <code>null</code> disables it. <code>(false, 2)</code> is also disabled.</td>
    </tr>
  </tbody>
</table>
</div>

## The Importance of `BambookLanguage`

`BambookLanguage` isn't just a hint—it directly dictates how punctuation is rendered to meet standard typesetting rules for different regions. Plus, it **automatically sets the `Locale` for the underlying `TextStyle`**, helping Flutter pick the right font and ensuring your characters look crisp.

- **`BambookLanguage.tc` (Traditional Chinese)**:
  - Punctuation (like `，`, `。`) is placed in the **center** of the character box.
  - Automatically sets `Locale('zh', 'Hant')`.

- **`BambookLanguage.sc` (Simplified Chinese)**:
  - Punctuation is placed in the **top-right** corner of the character box.
  - Automatically sets `Locale('zh', 'CN')`.

- **`BambookLanguage.jp` (Japanese)**:
  - Punctuation is placed in the **top-right** corner of the character box.
  - Automatically sets `Locale('ja', 'JP')`.

- **`BambookLanguage.kr` (Korean)**:
  - Punctuation is placed in the **top-right** corner of the character box.
  - Automatically sets `Locale('ko', 'KR')`.

Setting this correctly ensures your layout visually matches the reading habits of your target audience and gets the most accurate font rendering. **However**, on <mark>some Android systems</mark>, you might see <mark>correct font loading</mark> but <mark>incorrect punctuation positioning</mark>. So, if you're on Android and not using a custom font, we highly recommend setting `punctuationFixMode` to `force` to keep things looking sharp.

## Code Example

Check out the `example` folder in the project for more.

```dart
import 'package:flutter/material.dart';
import 'package:bambook/bambook.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
void main() {
  runApp(const BambookDemo());
}

class BambookDemo extends StatefulWidget {
  const BambookDemo({super.key});

  @override
  State<BambookDemo> createState() => _BambookDemoState();
}

class _BambookDemoState extends State<BambookDemo> {
  double _textHeight = 400;
  final double _minHeight = 200.0;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Bambook Vertical Typesetting Test')),
        body: LayoutBuilder(
          builder: (context, constraints) {
            final double availableHeight = constraints.maxHeight - 220;
            return Container(
              width: double.infinity,
              height: double.infinity,
              padding: const EdgeInsets.all(20),
              color: Colors.white,
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.center,
                children: [
                  const SizedBox(height: 20),
                  Align(
                    alignment: Alignment.center,
                    child: Container(
                      height: _textHeight > availableHeight
                          ? availableHeight
                          : _textHeight,
                      constraints: const BoxConstraints(maxWidth: 360),
                      decoration: const BoxDecoration(border: null),
                      alignment: Alignment.center,
                      child: const BambookText(
                        "Seasons change, sun and moon revolve, only the ink remains as solid as stone. --TwinType",
                        style: TextStyle(
                          fontSize: 22,
                          color: Color.fromARGB(255, 8, 19, 76),
                          fontFamily: 'LINESeed-TW_Rg',
                        ),

                        textAlign: BambookTextAlign.justify, /// Text alignment
                        language: BambookLanguage.tc, /// Language mode, affects punctuation style
                        direction:BambookTextDirection.rtl,
                        orientation: BambookTextOrientation.mixed, /// Latin handling mode
                        applyKinsoku: true, /// Line breaking rules (Kinsoku)
                        tateChuYoko: (false, 0), /// Tate-chu-yoko
                        punctuationFixMode:PunctuationFixMode.auto, /// CJK font fix, enable if system font doesn't support CJK vertical punctuation
                        lineSpacing: 24.0, /// Vertical line spacing
                        letterSpacing: -10, /// Vertical character spacing
                      ),
                    ),
                  ),
                  GestureDetector(
                    behavior: HitTestBehavior.translucent,
                    onVerticalDragUpdate: (details) {
                      setState(() {
                        _textHeight += details.delta.dy;
                        if (_textHeight < _minHeight) _textHeight = _minHeight;
                        if (_textHeight > availableHeight) {
                          _textHeight = availableHeight;
                        }
                      });
                    },
                    child: Container(
                      width: double.infinity,
                      height: 48,
                      alignment: Alignment.center,
                      child: const Icon(Icons.drag_handle, color: Colors.grey),
                    ),
                  ),
                  const Spacer(),
                  const Text(
                    "Powered By TwinType",
                    style: TextStyle(
                      color: Colors.grey,
                      fontSize: 12,
                      letterSpacing: 1.2,
                    ),
                  ),
                ],
              ),
            );
          },
        ),
      ),
    );
  }
}

```
<div class="img1">
    <img src="/assets/images/002.gif" alt="Preview" class="showImage">
</div>

## Disclaimer
This package is still in an early stage of development. East Asian typography is complex, and while we aim to cover most common use cases, we're still improving things. We can't guarantee correctness in every weird scenario (like mixing Japanese with Icelandic... wild!). Please manually verify your layout results, especially for critical uses like children's education.

If you're a linguistics or typography expert, we'd love your feedback!

This project is part of the Typexedra initiative, supported and maintained by TwinType. Submit issues for bugs or feature requests. Hope Bambook helps you build cool stuff! Any questions? Just ask.


## License

This package is **open source under the MIT License**. Please read the full license text and abide by it.

Copyright (C) <year> <copyright holders>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Notes
1. `V0.0.4` is our first public release. 0.0.1~0.0.3 were internal alpha builds. This doc is for `Bambook v0.0.4`.

2. This project is a sub-project of Typexedra, maintained by [TwinType][1]. For bugs or features, submit an issue. If you're a tech or language expert, join our discussion! Share via GitHub or email: Willy@twintyp.co. Much appreciated!

3. Check out the next chapter: **Glossary and Typography Guide** to learn more about vertical text and Bambook tricks.

[1]: https://twintype.co "TwinType"
