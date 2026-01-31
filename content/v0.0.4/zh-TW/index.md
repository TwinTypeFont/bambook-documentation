---
title: Bambook使用文件_V0.0.4
order: 0
slug: index
---


# Bambook 一款開源的Flutter垂直排版套件。

垂直文本對於中、日、韓、越以及蒙古文...等，十分常見，然Flutter中**卻未**提供垂直文本框。Bambook套件提供的相關方法，能夠使開發者快速配置垂直文本。

![垂直文本排版的可能，示意圖](assets/images/003.jpg)

pub.dev連結：<https://pub.dev/packages/bambook/>

## 開始使用

首先，請在您的 `pubspec.yaml` 檔案中加入 `bambook` 的依賴：

```yaml
dependencies:
  bambook: ^0.0.4 # 或更新
```

接著，在您的 Dart 程式碼中匯入套件：

```dart
import 'package:bambook/bambook.dart';
```

## `BambookText` 語法示意

`BambookText` 是本套件的核心 Widget，用法與 Flutter 原生的 `Text` Widget 非常相似。

```dart
const BambookText(
  "四季遞嬗，日月更迭，唯有筆墨如石堅。--TwinType",
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

## 參數詳解

以下是 `BambookText` 各個參數的詳細說明：

<div style="overflow-x:scroll;">
<table>
  <thead>
    <tr>
      <th>參數名 (Parameter)</th>
        <th>中文名稱</th>
      <th>型別 (Type)</th>
      <th>預設值 (Default)</th>
      <th style="text-align: left; min-width: 600px;">說明 (Description)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>data</code></td>
      <td>文本值</td>
      <td><code>String</code></td>
      <td><strong>必填</strong></td>
      <td style="text-align: left">您想要顯示的文字內容。</td>
    </tr>
    <tr>
      <td><code>style</code></td>
      <td>樣式</td>
      <td><code>TextStyle?</code></td>
      <td><code>null</code></td>
      <td style="text-align: left">文字樣式，支援 <code>fontSize</code> 等屬性。</td>
    </tr>
    <tr>
      <td><code>textAlign</code></td>
      <td>文本對齊方法</td>
      <td><code>BambookTextAlign</code></td>
      <td><code>BambookTextAlign.top</code></td>
      <td style="text-align: left">設定<strong>單一行的垂直對齊方式</strong>。可選值有：<code>top</code> (頂端對齊)、<code>center</code> (置中對齊)、<code>bottom</code> (底端對齊)、<code>justify</code> (頂底齊行)。</td>
    </tr>
    <tr>
      <td><code>direction</code></td>
      <td>換行方向</td>
      <td><code>BambookTextDirection</code></td>
      <td><code>BambookTextDirection.rtl</code></td>
      <td style="text-align: left">設定<strong>換行方向</strong>。可選值有：<code>rtl</code> (由右至左換行，適用於傳統 CJK 書寫) 或 <code>ltr</code> (由左至右換行)。</td>
    </tr>
    <tr>
      <td><code>orientation</code></td>
      <td>拉丁與數字行中處理方法</td>
      <td><code>BambookTextOrientation</code></td>
      <td><code>BambookTextOrientation.mixed</code></td>
      <td style="text-align: left">此子Latin與數字的<strong>字符方向</strong>一共分為三種設定。第一：<code>mixed</code>將使其以組為單位順時針旋轉90度，第二：<code>upright</code> 則會讓其保持直立；第三：<code>tateChuYoko</code>此設定會使所有拉丁與數字變為橫排</td>
    </tr>
    <tr>
      <td><code>language</code></td>
      <td>語系</td>
      <td><code>BambookLanguage</code></td>
      <td><code>BambookLanguage.tc</code></td>
      <td style="text-align: left">
<strong>文種設定，這會影響標點符號的預設位置</strong>。<code>tc</code> (繁體中文) 會讓標點符號置中；而 <code>sc</code> (簡體中文)、<code>jp</code> (日文)、<code>kr</code> (韓文) 則會讓標點符號靠上對齊。這個設定是為了符合不同地區的排版習慣。</td>
    </tr>
    <tr>
      <td><code>applyKinsoku</code></td>
      <td>避頭尾</td>
      <td><code>bool</code></td>
      <td><code>true</code></td>
      <td style="text-align: left">是否啟用<strong>避頭尾規則 (Kinsoku)</strong>。開啟後，可以防止逗號、句號等標點符號出現在一行的開頭。</td>
    </tr>
    <tr>
      <td><code>lineSpacing</code></td>
      <td>行距</td>
      <td><code>double</code></td>
      <td><code>10.0</code></td>
      <td style="text-align: left">
<strong>額外欄間距</strong>。設定<strong>欄與欄之間</strong>額外增加的空白距離 (邏輯像素 px)。<br><strong>警告：</strong> 建議您不要使用<code>text.style</code>中的<code>height</code>，或將其設為<code>1</code>因其為Flutter預設文本的參數，套用到Bambook後會導致錯誤。
</td>
    </tr>
    <tr>
      <td><code>letterSpacing</code></td>
      <td>字元間距</td>
      <td><code>double</code></td>
      <td><code>0.0</code></td>
      <td style="text-align: left">
<strong>垂直字元間距</strong>。設定<strong>同一行中</strong>每個字元之間的額外垂直距離。<br><strong>警告：</strong>請勿使用 <code>style.letterSpacing</code>，因為它會導致字元<strong>水平變寬</strong> (行寬變大)，而非增加垂直間距。若要調整直排字距，請務必使用此參數。</td>
    </tr>
    <tr>
      <td><code>punctuationFixMode</code></td>
      <td>標點位置修正</td>
      <td><code>PunctuationFixMode</code></td>
      <td><code>PunctuationFixMode.auto</code></td>
      <td style="text-align: left">
<strong>標點符號修正模式</strong>。由於不同作業系統（特別是 Android）對 CJK 字體的支援度不一，部分字體的標點符號（如逗號、句號）在垂直排版時可能會偏離中心線。此參數用於修正此問題：<br>- <code>auto</code>：會根據您是否配置字體為依據<br>- <code>force</code>：強制啟用修正。<br>- <code>disable</code>：停用修正。若您已使用自訂字體（如 <code>Noto Sans TC</code>）或在 iOS/macOS 開發，建議設為 <code>disable</code> 以獲得最佳效能與效果。</td>
    </tr>
    <tr>
      <td><code>tateChuYoko</code></td>
      <td>縱中橫例外處理</td>
      <td><code>(bool, int)?</code></td>
      <td><code>null</code></td>
      <td style="text-align: left">
<strong>縱中橫 (Tate-chu-yoko)</strong> 功能。當設定為 <code>(bool, N)</code> 時，長度<strong>小於或等於 N</strong> 的連續西文或數字會自動轉為橫向排列，嵌入在垂直文字流中。例如，<code>tateChuYoko: (true, 2)</code> 會讓 “A1”、”25” 等字串橫排顯示。若為 <code>null</code> 則停用此功能。如果設為<code>(false, 2)</code>仍為關閉。</td>
    </tr>
  </tbody>
</table>
</div>

## `BambookLanguage` 的重要性

`BambookLanguage` 參數不僅僅是一個提示，它會直接影響標點符號的渲染方式，以符合不同語區的標準排版規範。此外，它還會**自動為底層的 `TextStyle` 設定對應的 `Locale`**，這有助於 Flutter 選擇更適合該語言的字體，進而影響字符的實際顯示效果。

- **`BambookLanguage.tc` (繁體中文)**：
  - 標點符號（如 `，`、`。`）會被放置在字元的**正中央**。
  - 自動設定 `Locale('zh', 'Hant')`。

- **`BambookLanguage.sc` (簡體中文)**：
  - 標點符號會被放置在字元框的**右上角**。
  - 自動設定 `Locale('zh', 'CN')`。

- **`BambookLanguage.jp` (日文)**：
  - 標點符號會被放置在字元框的**右上角**。
  - 自動設定 `Locale('ja', 'JP')`。

- **`BambookLanguage.kr` (韓文)**：
  - 標點符號會被放置在字元框的**右上角**。
  - 自動設定 `Locale('ko', 'KR')`。

正確設定此參數，能確保您的排版結果在視覺上更貼近目標讀者的閱讀習慣，並獲得更精準的字體渲染。唯<mark>該設定在部分 Android 系統</mark>上出現<mark>字體調用正確</mark>，但<mark>標點錯誤</mark>之情況，因此如果您使用 Android 平台且未自定義字體，強力建議您將 `punctuationFixMode` 設為 `force` 以確保顯示正確。


## 語法範例

請參閱專案中`example`資料夾下範例

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
        appBar: AppBar(title: const Text('Bambook 垂直排版測試')),
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
                        "四季遞嬗，日月更迭，唯有筆墨如石堅。--TwinType",
                        style: TextStyle(
                          fontSize: 22,
                          color: Color.fromARGB(255, 8, 19, 76),
                          fontFamily: 'LINESeed-TW_Rg',
                        ),

                        textAlign: BambookTextAlign.justify, /// 文本對齊
                        language: BambookLanguage.tc, /// 文種模式，目前涉及標點樣式
                        direction:BambookTextDirection.rtl,
                        orientation: BambookTextOrientation.mixed, /// latin處理模式
                        applyKinsoku: true, /// 避頭尾
                        tateChuYoko: (false, 0), /// 縱中橫
                        punctuationFixMode:PunctuationFixMode.auto, /// CJK預設字體修正，如果您未安裝對應語言字型，建議開啟
                        lineSpacing: 24.0, /// 垂直行距
                        letterSpacing: -10, /// 垂直字元間距
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
    <img src="/assets/images/002.gif" alt="預覽" class="showImage">
</div>

## 警語
本套件仍處於前期開發階段，且東亞語系十分複雜，我們致力於盡量貼近多數使用情境，目前仍在持續改進中，無法保證在所有情況下皆正確，例如：日文與冰島語混排。請您務必自行核對排版結果是否正確，特別是在涉及孩童教育等重要用途時。

如您是語言或字體排印相關領域的專家，歡迎與我們聯繫提供建議與指正。

本項目為 Typexedra 計畫之一，由 TwinType 支持與維護。錯誤或功能請求請提交 issue。希望這份文件能幫助您更順利地使用 Bambook！如有任何問題，歡迎隨時提出。


## 授權

本套件採用**MIT授權條款開源**，請確保閱讀完整授權資訊，並遵守其規範。

Copyright (C) <year> <copyright holders>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## 備註
1. `V0.0.4`為首個正是面向公眾之版本，0.0.1~0.0.3為內部測試版本。此文件對應`Bamnook v0.0.4`。

2. 本項目為Typexedra之子計畫之一，由[TwinType][1]支持與維護。錯誤或功能請求請提交 issue。如果您是技術或語言專案，歡迎您加入討論與分享，您可以透過Github或連繫：Willy@twintyp.co。十分感恩！

3. 您可參閱下章節：**名詞解釋與排應說明**了解更多排印與Bambook使用技巧。

[1]: https://twintype.co "TwinType"
