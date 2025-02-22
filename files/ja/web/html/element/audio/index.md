---
title: '<audio>: 埋め込み音声要素'
slug: Web/HTML/Element/audio
---
{{HTMLRef}}

**HTML の `<audio>` 要素**は、文書内に音声コンテンツを埋め込むために使用します。この要素は、1 つまたは複数の音源を含むことができます。音源は `src` 属性または {{HTMLElement("source")}} 要素を使用して表し、ブラウザーがもっとも適切な音源を選択します。また、 {{domxref("MediaStream")}} を使用してストリーミングメディアを指し示すこともできます。

{{EmbedInteractiveExample("pages/tabbed/audio.html","tabbed-standard")}}

上記の例は、 `<audio>` 要素の単純な使用方法を示しています。 {{htmlelement("img")}} 要素と同様の方法で、埋め込みたいメディアへのパスを `src` 属性に設定します。他にも自動再生や繰り返しを行うかどうか、ブラウザーの既定のオーディオコントロールを表示したいかどうか、などの情報を指定する属性を含めることができます。

開始および終了タグ `<audio></audio>` の中のコンテンツは、この要素に対応してないブラウザーで代替として表示されます。

## 属性

この要素には[グローバル属性](/ja/docs/Web/HTML/Global_attributes)があります。

- {{htmlattrdef("autoplay")}}

  - : 論理属性。指定された場合、音声ファイル全体のダウンロードの完了を待たずに、再生可能な状態になった時点で即座にコンテンツの再生が始まります。

    > **Note:** 自動的に音声 (あるいは音声トラックを含む動画) を再生するサイトはユーザーにとって不快な体験になる可能性がありますので、可能な限り避けるべきです。自動再生機能が必須である場合は、オプトイン (ユーザーが明示的に有効化することを求める) にするべきです。ただし、ユーザーの制御下で後からソースを設定するメディア要素を作成するときは、この方法が役に立つでしょう。[自動再生ガイド](/ja/docs/Web/Media/Autoplay_guide)には autoplay の正しい使い方についての追加情報があります。

- {{htmlattrdef("controls")}}
  - : この属性が指定された場合、ブラウザーは再生・一時停止、音量、シークの各機能を制御するコントロールを表示します。
- {{htmlattrdef("crossorigin")}}

  - : この列挙型の属性は、関連する音声ファイルを取得する際に CORS を使用するかを示します。[CORS が有効なリソース](/ja/docs/CORS_Enabled_Image) は、*汚染*されることなく {{HTMLElement("canvas")}} 要素で再利用できます。次の値が使用できます:

    - `anonymous`
      - : 資格情報を伴わずにオリジン間リクエストを実行します。すなわち、 Cookie や X.509 証明書がない `Origin:` HTTP ヘッダーを送信する、あるいは HTTP ベーシック認証を行いません。サーバーが元のサイトに信用情報を付与しない場合 (`Access-Control-Allow-Origin:` HTTP ヘッダーの設定なし)、画像が*汚染*され、その使用も制限されます。
    - `use-credentials`
      - : 資格情報を伴ってオリジン間リクエストを実行します。すなわち、Cookie や X.509 証明書を伴う `Origin:` HTTP ヘッダーを送信する、あるいは HTTP ベーシック認証を行います。サーバーが元のサイトに信用情報を付与しない場合 (`Access-Control-Allow-Credentials:` HTTP ヘッダーに関わらず)、画像が*汚染*され、その使用も制限されます。

    この属性が存在しない場合、リソースは CORS リクエストなしで (すなわち、 `Origin:` HTTP ヘッダーなしで) 取得され、 {{HTMLElement('canvas')}} 要素での汚染されない使用が妨げられます。これが無効な場合、列挙型のキーワードに **anonymous** が指定されたものとして扱われます。追加の情報は [CORS 設定属性](/ja/docs/Web/HTML/CORS_settings_attributes) を参照してください。

- {{htmlattrdef("currentTime")}}

  - : `currentTime` を読み取ると、倍精度浮動小数点値で、現在の音声の再生位置を秒単位で示す値を返します。音声のメタデータが利用できない場合—この場合はメディアの開始時刻や長さを知ることができなくなるので— `currentTime` は再生が始まる時刻を示したり、変更したりすることができます。そうでない場合は、 `currentTime` を設定すると現在の再生位置を指定された時刻に設定し、メディアが現在読み込まれていれば、その位置にシークします。

    音声がストリーミングである場合は、 {{Glossary("user agent", "ユーザーエージェント")}} はデータがメディアバッファーからあふれた場合に一部を受け取ることができません。他にも音声が 0 秒から始まらないメディアタイムラインを持っている場合もあり、 `currentTime` をそれより前の時刻に設定すると失敗します。例えば、音声のメディアタイムラインが 12 時間目に始まる場合、 `currentTime` を 3600 に設定すると、現在の再生位置をメディアの開始位置の前に設定しようとするので、失敗します。 {{domxref("HTMLMediaElement.getStartDate", "getStartDate()")}} メソッドは、メディアのタイムラインの参照フレームの開始点を特定するのに使用することができます。

- {{htmlattrdef("disableRemotePlayback")}} {{experimental_inline}}

  - : 論理属性で、有線 (HDMI, DVI, など) や無線技術 (Mirachast, Chromecast, DLNA, AirPlay, など) で接続された機器のリモート再生機能を無効にするために使用します。詳しくは[この提案中の仕様書](https://www.w3.org/TR/remote-playback/#the-disableremoteplayback-attribute)をご覧ください。

    > **Note:** Safari では、代替として [`x-webkit-airplay="deny"`](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/AirPlayGuide/OptingInorOutofAirPlay/OptingInorOutofAirPlay.html) を使用することができます。

- {{htmlattrdef("duration")}} {{ReadOnlyInline}}
  - : 倍精度浮動小数点値で、メディアのタイムライン上の音声の長さ (合計の長さ) を秒単位で示します。要素上にメディアがない場合や、メディアが有効でない場合は、返値は `NaN` になります。メディアの終わりが分からない場合 (長さの分からないライブストリーミング、ウェブラジオ、 [WebRTC](/ja/docs/Web/API/WebRTC_API) から来たメディアなど)、この値は `+Infinity` になります。
- {{htmlattrdef("loop")}}
  - : 論理型の属性です。指定された場合、音声プレイヤーは音声の末尾に達すると、自動的に先頭に戻ります。
- {{htmlattrdef("muted")}}
  - : 論理型の属性で、音声の既定の設定を示します。この属性を設定すると、初期状態が消音になります。既定値は `false` です。
- {{htmlattrdef("preload")}}

  - : 列挙型の属性で、ユーザーに取って最良の結果をもたらすと作者が考えていることのヒントをブラウザーに伝えるためのものです。以下の値のうちひとつを持つことができます。

    - `none`: 音声を事前に読み込むべきではないことを示します。
    - `metadata`: 音声のメタデータ (例えば、長さ) を読み込みます。
    - `auto`: ユーザーが音声ファイルを使用しないと思われる場合でも、ファイル全体をダウンロードしてよいことを示します。
    - _空文字列_: これは `auto` 値と同義です。

    既定値はブラウザーによって異なります。仕様書では `metadata` にするよう助言しています。

    > **Note:** **使用上のメモ:**- `autoplay` 属性は `preload` より優先します。`autoplay` を指定すると、言うまでもなくブラウザーは音声を再生するためにダウンロードを始めなければなりません。
    >
    > - 仕様書は、ブラウザーがこの属性の値に従うことを強制していません。これは単なるヒントです。

- {{htmlattrdef("src")}}
  - : 埋め込む音声コンテンツの URL を指定します。なお、この属性は [HTTP access controls](/ja/docs/HTTP_access_control) に従います。この属性を省略し、audio 要素の子要素として配置した {{htmlelement("source")}} 要素とその src 属性を用いて指定することも可能であり、その場合、これを複数設置することで、異なるタイプの複数の代替コンテンツを配置することが可能となります。

## イベント

| イベント名                                                                                   | 発生する時                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {{Event("audioprocess")}}                                                             | {{DOMxRef("ScriptProcessorNode")}} の入力バッファが処理可能になった。                                                                                                                                                         |
| {{domxref("HTMLMediaElement.canplay_event", 'canplay')}}                 | ブラウザーがメディアを再生できるようになったものの、追加のバッファリングのために停止することなくメディアの最後まで再生するには、充分なデータが読み込まれていないとみられる。                                                            |
| {{domxref("HTMLMediaElement.canplaythrough_event", 'canplaythrough')}} | ブラウザーがコンテンツのバッファリングのために停止することなく最後までメディアを再生することができるとみられる。                                                                                                                        |
| {{Event("complete")}}                                                                 | {{DOMxRef("OfflineAudioContext")}} のレンダリングが終了した。                                                                                                                                                                 |
| {{domxref("HTMLMediaElement.durationchange_event", 'durationchange')}} | `duration` 属性が更新された。                                                                                                                                                                                                           |
| {{domxref("HTMLMediaElement.emptied_event", 'emptied')}}                 | メディアが空になった。例えば、このイベントはメディアがすでに読み込まれた (または部分的に読み込まれた) 状態で、再読み込みのために [`load()`](/ja/docs/XPCOM_Interface_Reference/NsIDOMHTMLMediaElement) メソッドが呼び出された場合など。 |
| {{domxref("HTMLMediaElement.ended_event", 'ended')}}                         | メディアの末尾に達したために再生が停止した。                                                                                                                                                                                            |
| {{domxref("HTMLMediaElement.loadeddata_event", 'loadeddata')}}         | メディアの最初のフレームが読み込み終わった。                                                                                                                                                                                            |
| {{domxref("HTMLMediaElement.loadedmetadata_event", 'loadedmetadata')}} | メタデータを読み込んだ。                                                                                                                                                                                                                |
| {{domxref("HTMLMediaElement.pause_event", 'pause')}}                         | 再生が一時停止した。                                                                                                                                                                                                                    |
| {{domxref("HTMLMediaElement.play_event", 'play')}}                         | 再生が始まった。                                                                                                                                                                                                                        |
| {{domxref("HTMLMediaElement.playing_event", 'playing ')}}                 | データがなくなったために一時停止または遅延した後で、再生の再開の準備ができた。                                                                                                                                                          |
| {{domxref("HTMLMediaElement.ratechange_event", 'ratechange')}}         | 再生レートが変更された。                                                                                                                                                                                                                |
| {{domxref("HTMLMediaElement.seeked_event", 'seeked')}}                     | *シーク*操作が完了した。                                                                                                                                                                                                                |
| {{domxref("HTMLMediaElement.seeking_event", 'seeking')}}                 | *シーク*操作が始まった。                                                                                                                                                                                                                |
| {{domxref("HTMLMediaElement.stalled_event", 'stalled')}}                 | ユーザーエージェントがメディアを読み込もうとしているが、データが予期せずに入ってこない。                                                                                                                                                |
| {{domxref("HTMLMediaElement.suspend_event", 'suspend')}}                 | メディアデータの読み込みが停止した。                                                                                                                                                                                                    |
| {{domxref("HTMLMediaElement.timeupdate_event", 'timeupdate')}}         | `currentTime` 属性で示されている時刻が更新された。                                                                                                                                                                                      |
| {{domxref("HTMLMediaElement.volumechange_event", 'volumechange')}}     | 音量が変更された。                                                                                                                                                                                                                      |
| {{domxref("HTMLMediaElement.waiting_event", 'waiting')}}                 | 一時的なデータの不足により、再生が停止した。                                                                                                                                                                                            |

## 使用上のメモ

ブラウザーはすべてが同じ[ファイル形式](/ja/docs/Web/Media/Formats/Containers)および[音声形式](/ja/docs/Web/Media/Formats/Audio_codecs)に対応しているわけではありません。内部に含められた {{htmlelement("source")}} 要素で複数のソースを提供することができ、ブラウザーは理解できる最初のものを使用します。

```html
<audio controls>
  <source src="myAudio.mp3" type="audio/mpeg">
  <source src="myAudio.ogg" type="audio/ogg">
  <p>Your browser doesn't support HTML5 audio. Here is
     a <a href="myAudio.mp4">link to the audio</a> instead.</p>
</audio>
```

私たちは大量の綿密な[メディアファイル形式](/ja/docs/Web/Media/Formats)と[その中で使用することができる音声コーデックのガイド](/ja/docs/Web/Media/Formats/Audio_codecs)を提供しています。また、[動画で対応しているコーデックのガイド](/ja/docs/Web/Media/Formats/Video_codecs)も利用することができます。

他の使用上のメモ:

- `controls` 属性を指定しない場合、音声プレイヤーはブラウザーの既定のコントロールを含めません。 JavaScript と {{domxref("HTMLMediaElement")}} API を使用して、独自のカスタムコントロールを作成することができます。
- 音声コンテンツを詳細に制御できるように、 `HTMLMediaElement` はさまざまな[イベント](/ja/docs/Web/Guide/Events/Media_events)を発行します。これは音声の読み込みプロセスを監視する方法も提供するので、エラーを監視したり、再生や捜査を始めることができるようになったことを検出したりすることができます。
- [Web Audio API](/ja/docs/Web/API/Web_Audio_API) を使用すると、既存の音声ファイルのストリーミングではなく、 JavaScript コードから音声ストリームを直接生成および操作することもできます。
- `<audio>` 要素は `<video>` 要素と同じような方法で字幕を持つことができません。 Ian Devlin による [WebVTT and Audio](https://www.iandevlin.com/blog/2015/12/html5/webvtt-and-audio) で、役立つ情報や作業があります。

HTML の `<audio>` 要素の使用に関する良い情報源として、[映像および音声コンテンツ](/ja/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)の初心者向けチュートリアルがあります。

### CSS でのスタイル付け

`<audio>` 要素は既定では固有の視覚的な出力を持ちませんが、 `controls` 属性が指定されると、ブラウザーの標準のコントロールが表示されます。

既定のコントロールは {{cssxref("display")}} の値に既定で `inline` を持っており、テキストブロックなどの中に置いておきたい場合でない限り、配置やレイアウトを制御しやすくするために、値を `block` に設定することは、多くの場合は良い考えです。

既定のコントロールは、ブロックを単位としてて影響するプロパティでスタイル付けすることができるので、 {{cssxref("border")}} や {{cssxref("border-radius")}}, {{cssxref("padding")}}, {{cssxref("margin")}} 等を指定することができます。しかし、音声プレイヤー内の個別のコンポーネントはスタイル付けすることができず (例えば、ボタンの寸法やアイコンの変更、フォントの変更など)、またコントロールはブラウザーごとに異なります。

ブラウザー間で一貫したルック＆フィールを実現するには、カスタムコントロールを作成する必要があるでしょう。これは好きな方法でマークアップおよびスタイル付けをすることができ、 JavaScript と {{domxref("HTMLMediaElement")}} API を使用することで、これらの機能を結合することができます。

[動画プレイヤーのスタイル付けの基本](/ja/docs/Web/Apps/Fundamentals/Audio_and_video_delivery/Video_player_styling_basics)は、便利なスタイル付けテクニックをいくつか紹介しています。これは `<video>` の文脈で書かれたものですが、多くは `<audio>` にも同様に適用されます。

### トラックの追加と削除の検出

{{event("addtrack")}} および {{event("removetrack")}} イベントを用いると、 `<audio>` 要素でトラックが追加されたり削除されたりしたことを検出することができます。しかし、これらのイベントは `<audio>` 要素自身に直接送信されるわけではありません。代わりに、 `<audio>` の {{domxref("HTMLMediaElement")}} 内にある、要素に追加されたトラックの種類に対応するトラックリストオブジェクトに送信されます。

- {{domxref("HTMLMediaElement.audioTracks")}}
  - : メディア要素のオーディオトラックのすべてを含む {{domxref("AudioTrackList")}} です。 `addtrack` のリスナーをこのオブジェクトに追加すると、新しいオーディオトラックが要素に追加された時に通知を受け取ることができます。
- {{domxref("HTMLMediaElement.videoTracks")}}
  - : この {{domxref("VideoTrackList")}} オブジェクトに `addtrack` リスナーを追加することで、要素に動画トラックが追加されたときに通知を受け取ることができます。
- {{domxref("HTMLMediaElement.textTracks")}}
  - : この {{domxref("TextTrackList")}} オブジェクトに `addtrack` リスナーを追加することで、要素にテキストトラックが追加されたときに通知を受け取る k とができます。

> **Note:** **メモ:** `<audio>` 要素であっても、動画やテキストトラックリストを持っており、インターフェイスの実装の使用が奇妙に見えますが、実際に動画を表示するために使用することができます。

例えば、次のようなコードで `<audio>` 要素で音声トラックが追加されたり削除されたりしたときを検出することができます。

```js
var elem = document.querySelector("audio");

elem.audioTrackList.onaddtrack = function(event) {
  trackEditor.addTrack(event.track);
};

elem.audioTrackList.onremovetrack = function(event) {
  trackEditor.removeTrack(event.track);
};
```

このコードは音声トラックが要素で追加および削除されることを監視し、トラックエディターの論理関数を呼び出すことで、エディターにおける利用できるトラックの一覧でトラックを登録や削除を行います。

{{event("addtrack")}} および {{event("removetrack")}} イベントを監視するには、 {{domxref("EventTarget.addEventListener", "addEventListener()")}} を使用することもできます。

## 例

### 基本的な使用法

以下の例は `<audio>` 要素で OGG ファイルを再生する単純な例を示しています。ページで許可されていれば、 `autoplay` 属性によって自動再生され、代替コンテンツも含んでいます。

```html
<!-- シンプルな音声再生 -->
<audio
  src="AudioTest.ogg"
  autoplay>
  あなたのブラウザーは <code>audio</code> 要素に対応していません。
</audio>
```

いつ自動再生が動作するのか、自動再生を使用する許可の取得方法、いつどのように自動再生を使用するのが適切であるのかについては、[自動再生ガイド](/ja/docs/Web/Media/Autoplay_guide)をご覧ください。

### \<source> 要素を伴う \<audio> 要素

この例では、埋め込まれる音声トラックを、 `<audio>` 要素の直接の `src` 属性ではなく、内部の `<source>` 要素のものを使用して指定しています。これは `type` 属性の中でファイルの MIME タイプを含めることで、ブラウザーがそのファイルを再生できるかどうかを知ることができ、そのファイル再生できないときに時間を浪費しません。

```html
<audio controls>
  <source src="foo.wav" type="audio/wav">
  あなたのブラウザーは <code>audio</code> 要素に対応していません。
</audio>
```

### 複数の \<source> 要素を持つ \<audio>

この例は複数の `<source>` 要素を含んでいます。ブラウザーは最初の source 要素 (Opus) を読み込もうとします。再生することができれば、2 番目 (vorbis) と 3 番目 (mp3) の読み込みは行われません。

```html
<audio controls>
 <source src="foo.opus" type="audio/ogg; codecs=opus"/>
 <source src="foo.ogg" type="audio/ogg; codecs=vorbis"/>
 <source src="foo.mp3" type="audio/mpeg"/>
</audio>
```

## アクセシビリティの考慮事項

台詞のある音声には、実際にコンテンツを説明する字幕と文字化情報 (transcript) を提供するべきです。 [WebVTT](/ja/docs/Web/API/WebVTT_API) を使用して字幕を指定すると、聴力を失った人が、音声の再生時に音声の内容を理解する事ができるようになるのに対し、文字化情報を使用すると、録音されたコンテンツを理解するのに時間が掛かる人が、自分に合ったペースと書式で録音の内容を確認できるようになります。

自動字幕サービスが使用されている場合は、生成されたコンテンツが元の音声を正しく表現しているかを確認することが重要です。

`<audio>` 要素は直接 WebVTT に対応していません。機能を提供するライブラリまたはフレームワークを探すか、字幕を表示するコードを自分自身で書くかする必要があります。一つの選択肢として、 {{HTMLElement("video")}} 要素が WebVTT に対応しているので、これで音声を再生するというものもあります。

字幕や文字化情報では、話されるセリフに加えて、重要な情報を伝える音楽や音響効果も識別できるようにしてください。これには感情や口調も含みます。例えば、以下の WebVTT では、角括弧を使用して口調や感情を閲覧者に示しています。これによって音楽、物音、効果音などの雰囲気を確立するのに役立ちます。

```
1
00:00:00 --> 00:00:45
[エネルギチックなテクノ音楽]

2
00:00:46 --> 00:00:51
タイムキーパーのポッドキャストのようこそ！このエピソードでは、私たちはどちらのスイス時計が腕時計かを議論します？

16
00:00:52 --> 00:01:02
[笑い] ごめん！言いたかったのは、どの腕時計がスイスの腕時計か？です。
```

また、 `<audio>` 要素に対応していないブラウザーを使用している閲覧者向けのフォールバックとしていくらかのコンテンツ (直接ダウンロードするリンクなど) を提供するのは良い習慣です。

```html
<audio controls>
  <source src="myAudio.mp3" type="audio/mpeg">
  <source src="myAudio.ogg" type="audio/ogg">
  <p>
    Your browser doesn't support HTML5 audio.
    Here is a <a href="myAudio.mp4">link to download the audio</a> instead.
  </p>
</audio>
```

- [MDN 字幕とクローズドキャプション - プラグイン](/ja/docs/Plugins/Flash_to_HTML5/Video/Subtitles_captions)
- [Web Video Text Tracks Format (WebVTT)](/ja/docs/Web/API/WebVTT_API)
- [WebAIM: Captions, Transcripts, and Audio Descriptions](https://webaim.org/techniques/captions/)
- [MDN WCAG を理解する ― ガイドライン 1.2 の解説](/ja/docs/Web/Accessibility/Understanding_WCAG/Perceivable#Guideline_1.2_—_Providing_text_alternatives_for_time-based_media)
- [Understanding Success Criterion 1.2.1 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
- [Understanding Success Criterion 1.2.2 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html)

## 技術的概要

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/ja/docs/Web/HTML/Content_categories">コンテンツカテゴリ</a>
      </th>
      <td>
        <a href="/ja/docs/Web/HTML/Content_categories#フローコンテンツ"
          >フローコンテンツ</a
        >、<a href="/ja/docs/HTML/Content_categories#記述コンテンツ"
          >記述コンテンツ</a
        >、<a href="/ja/docs/HTML/Content_categories#埋め込みコンテンツ"
          >埋め込みコンテンツ</a
        >。 {{htmlattrxref("controls", "audio")}}
        属性を持つ場合は、<a
          href="/ja/docs/HTML/Content_categories#対話型コンテンツ"
          >対話型コンテンツ</a
        >と<a href="/ja/docs/HTML/Content_categories#知覚可能コンテンツ"
          >知覚可能コンテンツ</a
        >。
      </td>
    </tr>
    <tr>
      <th scope="row">許可されている内容</th>
      <td>
        要素が {{htmlattrxref("src", "audio")}} 属性を持つ場合:
        0個以上の {{HTMLElement("track")}}
        要素とそれに続く、メディア要素を含まない透過的コンテンツ。すなわち
        {{HTMLElement("audio")}} 要素や {{HTMLElement("video")}}
        を子要素として配置してはなりません。<br />その他の場合: 0個以上の
        {{HTMLElement("source")}} 要素、0個以上の
        {{HTMLElement("track")}}
        要素、メディア要素を含まない透過的コンテンツ。すなわち
        {{HTMLElement("audio")}} 要素や {{HTMLElement("video")}}
        を子要素として配置してはなりません。
      </td>
    </tr>
    <tr>
      <th scope="row">タグの省略</th>
      <td>{{no_tag_omission}}</td>
    </tr>
    <tr>
      <th scope="row">許可されている親要素</th>
      <td>埋め込みコンテンツを受け入れるすべての要素。</td>
    </tr>
    <tr>
      <th scope="row">暗黙の ARIA ロール</th>
      <td>
        <a href="https://www.w3.org/TR/html-aria/#dfn-no-corresponding-role"
          >対応するロールなし</a
        >
      </td>
    </tr>
    <tr>
      <th scope="row">許可されている ARIA ロール</th>
      <td>{{ARIARole("application")}}</td>
    </tr>
    <tr>
      <th scope="row">DOM インターフェイス</th>
      <td>{{domxref("HTMLAudioElement")}}</td>
    </tr>
  </tbody>
</table>

## 仕様書

| 仕様書                                                                                                                           | 状態                             | 備考 |
| -------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- | ---- |
| {{SpecName('HTML WHATWG', 'embedded-content.html#the-audio-element', '&lt;audio&gt;')}}             | {{Spec2('HTML WHATWG')}} |      |
| {{SpecName('HTML5 W3C', 'semantics-embedded-content.html#the-audio-element', '&lt;audio&gt;')}} | {{Spec2('HTML5 W3C')}}     |      |

## ブラウザーの互換性

{{Compat("html.elements.audio")}}

## 関連情報

- [ウェブメディア技術](/ja/docs/Web/Media)

  - [メディアコンテナー形式 (ファイル形式)](/ja/docs/Web/Media/Formats/Containers)
  - [ウェブで使用される音声コーデックのガイド](/ja/docs/Web/Media/Formats/Audio_codecs)

- [Web Audio API](/ja/docs/Web/API/Web_Audio_API)
- {{domxref("HTMLAudioElement")}}
- {{htmlelement("source")}}
- {{htmlelement("video")}}
- [学習エリア: 動画及び音声のコンテンツ](/ja/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)
- [ブラウザーに依存しない音声の基本](/ja/Apps/Fundamentals/Audio_and_video_delivery/Cross-browser_audio_basics)
