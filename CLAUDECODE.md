# Lucid-SRD 販売サイト 開発仕様書

## プロジェクト概要

**Lucid-SRD**は、Sony Spatial Reality Display (ELF-SR2) 向けの医療用3D可視化アプリケーションです。
顎顔面外科手術の術前計画支援、DICOMデータの3D可視化、脳血管3Dモデルの可視化を実現します。
医療・研究機関（外科医、研究者、教育機関）をターゲットとしたB2B向けのプロフェッショナルな販売サイトを構築します。

---

## 技術仕様

### 使用技術
- **HTML5**: セマンティックHTMLによる構造化
- **Tailwind CSS**: CDN版を使用（v3.x系）
- **JavaScript**: バニラJS（軽量なインタラクション用）
- **フォント**: Google Fonts - Noto Sans JP

### 対応環境
- モダンブラウザ（Chrome, Firefox, Safari, Edge 最新版）
- レスポンシブ対応（モバイル: 320px〜, タブレット: 768px〜, デスクトップ: 1024px〜）

### ファイル構成
```
project/
├── index.html          # メインページ
├── terms.html          # 利用規約
├── tokusho.html        # 特定商取引法に基づく表記
├── privacy.html        # プライバシーポリシー
├── assets/
│   ├── images/         # 画像ファイル（ロゴ、製品画像など）
│   └── videos/         # 動画ファイル
└── CLAUDECODE.md       # この仕様書
```

---

## デザイン方針

### カラーパレット
- **プライマリー**: 濃い青 `#1e3a8a` (Tailwind: blue-900)
- **セカンダリー**: 中間の青 `#3b82f6` (Tailwind: blue-500)
- **背景**: 白 `#ffffff` + 薄いグレー `#f9fafb` (Tailwind: gray-50)
- **テキスト**: ダークグレー `#1f2937` (Tailwind: gray-800)
- **アクセント**: 明るい青 `#60a5fa` (Tailwind: blue-400)

### タイポグラフィ
- **見出し（H1）**: 3xl〜4xl, font-bold
- **見出し（H2）**: 2xl〜3xl, font-bold
- **見出し（H3）**: xl〜2xl, font-semibold
- **本文**: base〜lg, font-normal
- **行間**: leading-relaxed（1.625）

### デザイン原則
1. **清潔感**: 余白を十分に取り、情報を整理
2. **信頼性**: 医療・研究機関が安心できるプロフェッショナルな印象
3. **分かりやすさ**: 技術情報を平易に伝える
4. **アクション促進**: CTAボタンを適切に配置
5. **配色制約**: 赤色系統は使用しない（医療現場での警告色を避ける）

---

## ページ構成

### 1. ヒーローセクション
**目的**: 第一印象で製品の価値を伝え、訪問者の興味を引く

**要素**:
- キャッチコピー（H1）: 「立体を、ありのままに、快適に」
  - フォントサイズ: 4xl（モバイル）〜 6xl（デスクトップ）
  - 太字、中央揃え
- サブヘッドライン（H2）: 「空間再現ディスプレイを、臨床現場へ。」
  - フォントサイズ: xl〜2xl
- 背景: 動画プレースホルダーまたは高品質画像
  - 暗めのオーバーレイ（opacity-40）でテキストの可読性確保
  - ※実際の素材は後から差し替え
- CTAボタン: 2つ並列
  - プライマリー: 「詳しく見る」（スムーススクロール）
  - セカンダリー: 「お問い合わせ」（問い合わせセクションへ）
- 高さ: 画面の80vh〜100vh

**実装メモ**:
```html
<!-- 構造イメージ -->
<section class="relative h-screen flex items-center justify-center">
  <div class="absolute inset-0 bg-blue-900 opacity-40"></div>
  <video class="absolute inset-0 w-full h-full object-cover" ...></video>
  <div class="relative z-10 text-center text-white">
    <h1>立体を、ありのままに</h1>
    <p>サブヘッドライン</p>
    <div class="mt-8 flex gap-4">
      <button>詳しく見る</button>
      <button>今すぐ購入</button>
    </div>
  </div>
</section>
```

---

### 2. 製品特徴セクション
**目的**: 製品の主要な特徴とベネフィットを伝える

**構成**: 3〜4つの特徴を横並びカードで表示

**各カードの要素**:
- アイコン: SVGまたはUnicodeアイコン（例: 📐 🔬 ⚡）
- 見出し（H3）: 特徴の名称（例: 「高精度な3D表示」）
- 説明文: 2〜3行（80〜120文字程度）
- カードデザイン: 白背景、軽いシャドウ、ホバー時にリフトアップ

**レイアウト**:
- デスクトップ: 3〜4カラムグリッド
- タブレット: 2カラムグリッド
- モバイル: 1カラム縦積み

**実装例**:
```html
<section class="py-20 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12">製品の特徴</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <!-- カード1 -->
      <div class="bg-white p-8 rounded-lg shadow-md hover:shadow-xl transition">
        <div class="text-5xl mb-4">📐</div>
        <h3 class="text-xl font-semibold mb-3">高精度な3D表示</h3>
        <p class="text-gray-600">空間再現ディスプレイの特性を最大限に活用し、医療現場で求められる正確な立体表示を実現します。</p>
      </div>
      <!-- カード2, 3... -->
    </div>
  </div>
</section>
```

**提案する特徴（例）**:
1. **多彩なファイル形式に対応**
   - 説明: STL・OBJ・DICOMの主要な医療用ファイル形式に対応。既存のワークフローにシームレスに統合できます。
   
2. **スピーディな操作性**
   - 説明: 少ない工程と最小限の待ち時間で、すぐに3D可視化を実現。臨床現場での迅速な判断をサポートします。
   
3. **多様な操作方法**
   - 説明: マウス、ゲームパッド、フリーハンド（ジェスチャー）での操作に対応。直感的で快適な操作環境を提供します。

---

### 3. ユースケース・活用シーンセクション
**目的**: 具体的な利用シーンをイメージさせ、導入メリットを示す

**構成**: 2〜3つのユースケースを交互レイアウトで表示

**各ユースケースの要素**:
- 画像: プレースホルダー（640x480程度）
- 見出し（H3）: シーン名（例: 「手術計画での活用」）
- 説明文: 3〜5行
- レイアウト: 画像と文章を交互に左右配置

**実装例**:
```html
<section class="py-20">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12">活用シーン</h2>
    
    <!-- ユースケース1: 画像左 -->
    <div class="flex flex-col md:flex-row items-center gap-8 mb-16">
      <div class="md:w-1/2">
        <img src="placeholder-1.jpg" alt="手術計画" class="rounded-lg shadow-lg">
      </div>
      <div class="md:w-1/2">
        <h3 class="text-2xl font-semibold mb-4">手術計画での活用</h3>
        <p class="text-gray-600">説明文...</p>
      </div>
    </div>
    
    <!-- ユースケース2: 画像右 -->
    <div class="flex flex-col md:flex-row-reverse items-center gap-8">
      ...
    </div>
  </div>
</section>
```

**提案するユースケース（例）**:
1. **顎変形症の手術シミュレーション**
   - 説明文: 患者のCTデータから3Dモデルを作成し、術前計画を立体的に検討。空間再現ディスプレイの裸眼立体視により、骨格の位置関係を正確に把握できます。（※説明文は後で詳細化可能）
   
2. **解剖学教育での活用**
   - 説明文: 複雑な脳血管や顔面骨格の構造を、学生や研修医に立体的に提示。教科書では理解しにくい空間的な位置関係を、直感的に学習できます。（※説明文は後で詳細化可能）
   
3. **症例検討での活用**
   - 説明文: カンファレンスや症例検討会で、複数の医師が同時に立体画像を共有。手術アプローチや治療方針について、より具体的な議論が可能になります。（※説明文は後で詳細化可能）

---

### 4. 動作環境・スペックセクション
**目的**: 技術仕様を明確に伝え、導入検討の判断材料を提供

**構成**: 見やすい表形式

**項目**:
- 対応OS: Windows 10/11 (64bit)
- CPU: Intel Core i7-9700K以上推奨
- メモリ: 16GB以上
- GPU: NVIDIA GeForce RTX 3060以上
- 対応ディスプレイ: Sony Spatial Reality Display (ELF-SR2)
- ストレージ: SSD推奨、5GB以上の空き容量
- その他: ジェスチャーコントロール使用時は別途Webカメラが必要

**実装例**:
```html
<section class="py-20 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12">動作環境</h2>
    <div class="max-w-3xl mx-auto bg-white rounded-lg shadow-md overflow-hidden">
      <table class="w-full">
        <tbody>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50 w-1/3">対応OS</td>
            <td class="px-6 py-4">Windows 10/11 (64bit)</td>
          </tr>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50">CPU</td>
            <td class="px-6 py-4">Intel Core i7-9700K 以上推奨</td>
          </tr>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50">メモリ</td>
            <td class="px-6 py-4">16GB以上</td>
          </tr>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50">GPU</td>
            <td class="px-6 py-4">NVIDIA GeForce RTX 3060以上</td>
          </tr>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50">対応ディスプレイ</td>
            <td class="px-6 py-4">Sony Spatial Reality Display (ELF-SR2)</td>
          </tr>
          <tr class="border-b">
            <td class="px-6 py-4 font-semibold bg-blue-50">ストレージ</td>
            <td class="px-6 py-4">SSD推奨、5GB以上の空き容量</td>
          </tr>
          <tr>
            <td class="px-6 py-4 font-semibold bg-blue-50">その他</td>
            <td class="px-6 py-4">ジェスチャーコントロール使用時は別途Webカメラが必要</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</section>
```

---

### 5. 購入オプションセクション
**目的**: 販売形態を明確に示し、購入への導線を作る

**構成**: 2つのプランカードを横並び表示

**各カードの要素**:
- プラン名（H3）: 「ダウンロード版」「USB版」
- 価格表示: ¥400,000（税込）
- 特徴リスト: 3〜5項目（チェックマーク付き）
- 特典表示: DL版にはジェスチャーコントロールアプリ（¥20,000相当）同梱
- CTAボタン: 「お問い合わせ」
- カードデザイン: 枠線、ホバー時にハイライト
- 注意書き: 「※ご購入前に利用規約をご確認ください」のリンク

**実装例**:
```html
<section class="py-20">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-4">購入オプション</h2>
    <p class="text-center text-gray-600 mb-12">買い切りライセンスで長期的にご利用いただけます</p>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 max-w-4xl mx-auto">
      
      <!-- ダウンロード版 -->
      <div class="border-2 border-blue-500 rounded-lg p-8 hover:shadow-xl transition relative">
        <div class="absolute top-4 right-4 bg-blue-600 text-white px-3 py-1 rounded-full text-sm">
          おすすめ
        </div>
        <h3 class="text-2xl font-bold mb-4">ダウンロード版</h3>
        <div class="text-4xl font-bold text-blue-600 mb-2">¥400,000</div>
        <div class="text-sm text-gray-600 mb-6">（税込・買い切り）</div>
        
        <div class="bg-blue-50 p-3 rounded-lg mb-6">
          <p class="text-sm font-semibold text-blue-800">
            ✨ ジェスチャーコントロールアプリ同梱<br>
            <span class="text-xs">（¥20,000相当）</span>
          </p>
        </div>
        
        <ul class="space-y-3 mb-8">
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>購入後即ダウンロード可能</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>1年間の導入支援・サポート付き</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>無料アップデート対応</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>フリーハンド操作が可能</span>
          </li>
        </ul>
        <a href="#contact" class="block w-full bg-blue-600 text-white text-center py-3 rounded-lg hover:bg-blue-700 transition">
          お問い合わせ
        </a>
      </div>
      
      <!-- USB版 -->
      <div class="border-2 border-blue-200 rounded-lg p-8 hover:border-blue-500 hover:shadow-xl transition">
        <h3 class="text-2xl font-bold mb-4">USB版</h3>
        <div class="text-4xl font-bold text-blue-600 mb-2">¥400,000</div>
        <div class="text-sm text-gray-600 mb-6">（税込・買い切り）</div>
        
        <div class="h-14 mb-6"></div>
        
        <ul class="space-y-3 mb-8">
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>プロダクトキー入りUSBで配送</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>1年間の導入支援・サポート付き</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>無料アップデート対応</span>
          </li>
          <li class="flex items-start">
            <svg class="w-6 h-6 text-green-500 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>物理メディアでの保管が可能</span>
          </li>
        </ul>
        <a href="#contact" class="block w-full bg-blue-600 text-white text-center py-3 rounded-lg hover:bg-blue-700 transition">
          お問い合わせ
        </a>
      </div>
      
    </div>
    
    <!-- ライセンスオプション -->
    <div class="mt-12 max-w-4xl mx-auto bg-gray-50 p-6 rounded-lg">
      <h3 class="text-xl font-semibold mb-4 text-center">複数台でのご利用をお考えの方へ</h3>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div class="bg-white p-4 rounded-lg">
          <h4 class="font-semibold mb-2">シングルライセンス</h4>
          <p class="text-2xl font-bold text-blue-600 mb-2">¥400,000</p>
          <p class="text-sm text-gray-600">PC 1台につき1ライセンス</p>
        </div>
        <div class="bg-white p-4 rounded-lg">
          <h4 class="font-semibold mb-2">サイトライセンス</h4>
          <p class="text-2xl font-bold text-blue-600 mb-2">¥1,200,000</p>
          <p class="text-sm text-gray-600">同一組織内で最大5台まで</p>
        </div>
      </div>
    </div>
    
    <p class="text-center text-sm text-gray-600 mt-8">
      ※ご購入前に<a href="terms.html" class="text-blue-600 hover:underline">利用規約</a>をご確認ください
    </p>
  </div>
</section>
```

**注意事項**:
- 問い合わせボタンは#contactにリンク（お問い合わせセクションへスムーススクロール）
- 価格は税込表記
- 利用規約への明確なリンクを配置

---

### 6. FAQ（よくある質問）セクション
**目的**: 疑問を解消し、購入への心理的ハードルを下げる

**構成**: アコーディオン形式で5〜7項目

**実装**: JavaScriptで開閉機能を実装

**質問項目**:
1. **ライセンスの種類について**
   - 回答: シングルライセンス（PC1台・¥400,000）とサイトライセンス（同一組織内最大5台・¥1,200,000）をご用意しています。

2. **複数台での使用は可能ですか？**
   - 回答: サイトライセンスをご購入いただければ、同一組織内で最大5台までインストール可能です。

3. **サポート体制について**
   - 回答: ご購入から1年間、導入支援とサポートを提供いたします。メールでのお問い合わせに対応いたします。

4. **アップデートは無料ですか？**
   - 回答: Windowsアップデート等に伴うソフトウェアアップデートは無料で提供いたします。サイトからダウンロード可能です。

5. **返品・返金ポリシー**
   - 回答: ソフトウェアの性質上、原則として返品・返金は承っておりません。ご購入前に体験版をお試しいただくことをお勧めします。

6. **体験版はありますか？**
   - 回答: はい、特定のサンプルデータでお試しいただける体験版をご用意しています。お問い合わせフォームよりご連絡ください。

7. **医療機器としての認証について**
   - 回答: 本ソフトウェアは研究・教育・患者説明支援を目的としており、医療機器プログラム（SaMD）としての認証は受けておりません。診断や治療方針の決定は必ず医師の責任において行ってください。

**実装例**:
```html
<section class="py-20 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12">よくある質問</h2>
    <div class="max-w-3xl mx-auto space-y-4">
      
      <div class="bg-white rounded-lg shadow-md">
        <button class="w-full px-6 py-4 text-left flex justify-between items-center">
          <span class="font-semibold">ライセンスの種類について</span>
          <svg class="w-6 h-6 transform transition" ...>▼</svg>
        </button>
        <div class="px-6 pb-4 hidden">
          <p class="text-gray-600">回答文...</p>
        </div>
      </div>
      
      <!-- 他のFAQ項目 -->
    </div>
  </div>
</section>
```

---

### 7. お問い合わせセクション
**目的**: 直接的なコミュニケーションチャネルを提供

**構成オプション**:

**オプション1: シンプルなメールアドレス表示**
```html
<section class="py-20" id="contact">
  <div class="container mx-auto px-4 text-center">
    <h2 class="text-3xl font-bold mb-8">お問い合わせ</h2>
    <p class="text-lg mb-6">ご質問・ご相談、体験版のお申し込みはお気軽にお問い合わせください。</p>
    <a href="mailto:otuki.3104@gmail.com" class="text-blue-600 text-xl font-semibold hover:underline">
      otuki.3104@gmail.com
    </a>
  </div>
</section>
```

**オプション2: コンタクトフォーム**
```html
<section class="py-20 bg-gray-50" id="contact">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-4">お問い合わせ</h2>
    <p class="text-center text-gray-600 mb-12">ご質問・ご相談、体験版のお申し込みはこちらから</p>
    <form class="max-w-2xl mx-auto bg-white p-8 rounded-lg shadow-md">
      <div class="mb-6">
        <label class="block font-semibold mb-2">お名前 <span class="text-red-600">*</span></label>
        <input type="text" class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-blue-500" required>
      </div>
      <div class="mb-6">
        <label class="block font-semibold mb-2">メールアドレス <span class="text-red-600">*</span></label>
        <input type="email" class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-blue-500" required>
      </div>
      <div class="mb-6">
        <label class="block font-semibold mb-2">所属機関</label>
        <input type="text" class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-blue-500">
      </div>
      <div class="mb-6">
        <label class="block font-semibold mb-2">お問い合わせ種別 <span class="text-red-600">*</span></label>
        <select class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:border-blue-500" required>
          <option value="">選択してください</option>
          <option value="purchase">購入に関するお問い合わせ</option>
          <option value="trial">体験版のお申し込み</option>
          <option value="support">技術サポート</option>
          <option value="other">その他</option>
        </select>
      </div>
      <div class="mb-6">
        <label class="block font-semibold mb-2">お問い合わせ内容 <span class="text-red-600">*</span></label>
        <textarea class="w-full px-4 py-2 border rounded-lg h-32 focus:outline-none focus:border-blue-500" required></textarea>
      </div>
      <div class="mb-6">
        <label class="flex items-start">
          <input type="checkbox" class="mt-1 mr-2" required>
          <span class="text-sm text-gray-600">
            <a href="privacy.html" class="text-blue-600 hover:underline">プライバシーポリシー</a>に同意する
          </span>
        </label>
      </div>
      <button type="submit" class="w-full bg-blue-600 text-white py-3 rounded-lg hover:bg-blue-700 transition">
        送信する
      </button>
    </form>
    <div class="text-center mt-8">
      <p class="text-gray-600">メールでのお問い合わせ:</p>
      <a href="mailto:otuki.3104@gmail.com" class="text-blue-600 hover:underline">
        otuki.3104@gmail.com
      </a>
    </div>
  </div>
</section>
```

**注意**: フォームの実際の送信機能は後で実装（Netlify Forms、Formspreeなど）

---

### 8. フッターセクション
**目的**: サイト全体の情報を整理し、法的事項へのリンクを提供

**要素**:
- 会社情報/研究者情報
- リンク集（プライバシーポリシー、特定商取引法など）
- SNSアイコン（将来用、プレースホルダー可）
- コピーライト表記

**実装例**:
```html
<footer class="bg-gray-900 text-white py-12">
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
      
      <!-- 製品情報 -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Lucid-SRD</h3>
        <p class="text-gray-400 text-sm">
          空間再現ディスプレイを、臨床現場へ。<br>
          医療用3D可視化ソリューション
        </p>
      </div>
      
      <!-- リンク -->
      <div>
        <h3 class="text-lg font-semibold mb-4">リンク</h3>
        <ul class="space-y-2 text-gray-400 text-sm">
          <li><a href="terms.html" class="hover:text-white transition">利用規約</a></li>
          <li><a href="tokusho.html" class="hover:text-white transition">特定商取引法に基づく表記</a></li>
          <li><a href="privacy.html" class="hover:text-white transition">プライバシーポリシー</a></li>
        </ul>
      </div>
      
      <!-- 運営者情報 -->
      <div>
        <h3 class="text-lg font-semibold mb-4">運営者情報</h3>
        <p class="text-gray-400 text-sm">
          岡山大学病院<br>
          口腔顎顔面外科<br>
          〒700-8558<br>
          岡山県岡山市北区鹿田町2-5-1
        </p>
      </div>
      
    </div>
    
    <div class="border-t border-gray-800 pt-8 text-center text-gray-400 text-sm">
      <p>&copy; 2025 Lucid-SRD. All rights reserved.</p>
      <p class="mt-2">Sony Spatial Reality Display は Sony Corporation の商標です。</p>
    </div>
  </div>
</footer>
```

---

## SEO対策

### メタタグ設定

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- 基本SEO -->
  <title>Lucid-SRD - Sony Spatial Reality Display対応 医療用3D可視化アプリケーション</title>
  <meta name="description" content="立体を、ありのままに、快適に。空間再現ディスプレイ(ELF-SR2)で実現する医療用3D可視化ソリューション。顎顔面外科手術の術前計画、DICOM・STL・OBJ形式に対応。">
  <meta name="keywords" content="Lucid-SRD,空間再現ディスプレイ,Sony Spatial Reality Display,ELF-SR2,医療3D,DICOM,手術計画,顎顔面外科,脳神経外科,3D可視化">
  
  <!-- OGP (SNSシェア用) -->
  <meta property="og:title" content="Lucid-SRD - 医療用3D可視化アプリケーション">
  <meta property="og:description" content="立体を、ありのままに、快適に。空間再現ディスプレイを、臨床現場へ。">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://example.com/">
  <meta property="og:image" content="https://example.com/ogp-image.jpg">
  <meta property="og:site_name" content="Lucid-SRD">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Lucid-SRD - 医療用3D可視化アプリケーション">
  <meta name="twitter:description" content="立体を、ありのままに、快適に。">
  <meta name="twitter:image" content="https://example.com/twitter-image.jpg">
  
  <!-- Favicon -->
  <link rel="icon" type="image/png" href="assets/images/favicon.png">
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            'sans': ['Noto Sans JP', 'sans-serif'],
          },
        }
      }
    }
  </script>
</head>
```

### 構造化データ（JSON-LD）

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Lucid-SRD",
  "description": "Sony Spatial Reality Display (ELF-SR2) 向けの医療用3D可視化アプリケーション。顎顔面外科手術の術前計画支援、DICOMデータの3D可視化に対応。",
  "applicationCategory": "MedicalApplication",
  "operatingSystem": "Windows 10, Windows 11",
  "softwareRequirements": "Sony Spatial Reality Display (ELF-SR2)",
  "offers": {
    "@type": "Offer",
    "price": "400000",
    "priceCurrency": "JPY",
    "availability": "https://schema.org/InStock"
  },
  "provider": {
    "@type": "Organization",
    "name": "岡山大学病院 口腔顎顔面外科",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "鹿田町2-5-1",
      "addressLocality": "岡山市北区",
      "addressRegion": "岡山県",
      "postalCode": "700-8558",
      "addressCountry": "JP"
    }
  }
}
</script>
```

---

## JavaScript機能

### 必要なインタラクション

1. **スムーススクロール**
```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  });
});
```

2. **FAQアコーディオン**
```javascript
const faqButtons = document.querySelectorAll('.faq-button');
faqButtons.forEach(button => {
  button.addEventListener('click', () => {
    const content = button.nextElementSibling;
    const icon = button.querySelector('svg');
    content.classList.toggle('hidden');
    icon.classList.toggle('rotate-180');
  });
});
```

3. **ヘッダーの背景変化（スクロール時）**
```javascript
window.addEventListener('scroll', () => {
  const header = document.querySelector('header');
  if (window.scrollY > 100) {
    header.classList.add('bg-white', 'shadow-md');
  } else {
    header.classList.remove('bg-white', 'shadow-md');
  }
});
```

---

## パフォーマンス最適化

### 画像最適化
- 遅延読み込み: `loading="lazy"` 属性を使用
- 適切なフォーマット: WebP形式を推奨
- 解像度: レスポンシブ画像用に複数サイズを用意

```html
<img src="image.webp" 
     srcset="image-small.webp 480w, image-medium.webp 768w, image-large.webp 1200w"
     sizes="(max-width: 768px) 100vw, 50vw"
     alt="説明文"
     loading="lazy">
```

### CSS/JSの最適化
- Tailwind CDNは本番では最小化版を使用
- 不要なCSSは削除
- JavaScriptは最小限に

---

## アクセシビリティ

### 必須対応
1. **セマンティックHTML**: 適切なHTML5タグを使用
2. **altテキスト**: すべての画像に説明を付ける
3. **キーボード操作**: タブキーでの移動が可能
4. **コントラスト比**: WCAG AA基準（4.5:1以上）を満たす
5. **ARIAラベル**: 必要に応じてaria-label等を使用

```html
<!-- 良い例 -->
<button aria-label="メニューを開く" class="...">
  <svg aria-hidden="true">...</svg>
</button>
```

---

## 実装の優先順位

### フェーズ1: 基本構造（最優先）
1. HTML骨組み作成
2. Tailwind CSSでスタイリング
3. レスポンシブ対応

### フェーズ2: コンテンツ（高優先度）
1. 各セクションのコンテンツ作成
2. プレースホルダー画像の配置
3. SEOメタタグの設定

### フェーズ3: インタラクション（中優先度）
1. スムーススクロール実装
2. FAQアコーディオン実装
3. その他のアニメーション

### フェーズ4: 最適化（低優先度）
1. パフォーマンス最適化
2. アクセシビリティ改善
3. クロスブラウザテスト

---

## 将来の拡張予定

1. **決済システム統合**
   - Stripe, PayPalなどの導入
   - ライセンスキー自動発行システム

2. **CMS導入**
   - ブログ機能
   - 活用事例の追加

3. **多言語対応**
   - 英語版の作成
   - i18n対応

4. **ユーザーサポート**
   - チャットボット
   - サポートチケットシステム

---

## チェックリスト

実装完了時に以下を確認：

**基本機能**:
- [ ] すべてのセクションが実装されている
- [ ] レスポンシブデザインが機能している（モバイル/タブレット/デスクトップ）
- [ ] スムーススクロールが動作している
- [ ] FAQアコーディオンが動作している

**SEO対策**:
- [ ] SEOメタタグが設定されている
- [ ] 構造化データが実装されている
- [ ] OGP/Twitter Cardが設定されている
- [ ] 画像のalt属性が設定されている

**法務関連**:
- [ ] 利用規約ページ（terms.html）が作成されている
- [ ] 特定商取引法ページ（tokusho.html）が作成されている
- [ ] プライバシーポリシーページ（privacy.html）が作成されている
- [ ] 各法務ページへのリンクがフッターに配置されている
- [ ] 購入セクションに利用規約へのリンクがある
- [ ] お問い合わせフォームにプライバシーポリシーへのリンクがある

**コンテンツ**:
- [ ] 製品名「Lucid-SRD」が正しく表示されている
- [ ] 価格が正確に記載されている（¥400,000）
- [ ] 対応ディスプレイ「Sony Spatial Reality Display (ELF-SR2)」が明記されている
- [ ] お問い合わせメールアドレスが正しい

**リンク・ナビゲーション**:
- [ ] 内部リンクが正しく機能している
- [ ] お問い合わせセクションへのスムーススクロールが動作
- [ ] リンク切れがない

**技術的確認**:
- [ ] クロスブラウザで表示確認済み（Chrome, Firefox, Safari, Edge）
- [ ] モバイルで表示確認済み
- [ ] コンソールエラーがない
- [ ] ページ読み込み速度が適切

---

## 参考資料

### デザインリファレンス
- Tailwind CSS公式: https://tailwindcss.com/
- Google Fonts: https://fonts.google.com/

### SEOツール
- Google Search Console
- Google Analytics 4
- PageSpeed Insights

### ホスティング候補
- GitHub Pages
- Netlify
- Vercel

---

## 法務関連ページ

医療ソフトウェアの販売において、法的保護とユーザーへの情報開示は必須です。
以下の3つのページを作成します。

### 9. 利用規約（terms.html）

**目的**: ソフトウェアの使用条件、免責事項、ライセンス条件を明示

**必須記載事項**:
1. 非医療機器であることの明示
2. 使用目的の限定
3. 責任の制限
4. ライセンス条件
5. 知的財産権
6. 禁止事項
7. 保証の否認

**実装のポイント**:
- 「非医療機器である」ことを目立つ警告ボックスで強調
- 免責事項を明確に記載
- ライセンスの種類（シングル/サイト）を明記
- 読みやすいセクション分け

---

### 10. 特定商取引法に基づく表記（tokusho.html）

**目的**: 電子商取引における消費者保護のための情報開示

**必須記載事項**:
1. 販売業者: 岡山大学病院 口腔顎顔面外科
2. 運営責任者: [要確認]
3. 所在地: 〒700-8558 岡山県岡山市北区鹿田町2-5-1
4. 連絡先: otuki.3104@gmail.com
5. 販売価格: シングル¥400,000、サイト¥1,200,000（税込）
6. 支払方法: 銀行振込
7. 引渡時期: DL版は入金確認後3営業日、USB版は5営業日
8. 返品: 原則不可（不具合時のみ30日以内対応）

**実装のポイント**:
- 表形式で見やすく整理
- 返品ポリシーを明確に
- 医療機器でないことの注意書き

---

### 11. プライバシーポリシー（privacy.html）

**目的**: 個人情報の取り扱いについて明示

**必須記載事項**:
1. 収集する情報: 氏名、メール、所属、住所（USB版のみ）
2. 利用目的: 問い合わせ対応、購入手続き、サポート
3. 第三者提供: 原則なし（法令に基づく場合を除く）
4. 管理方法: セキュリティ対策の実施
5. Cookie使用: サイト改善のため使用する場合あり
6. お問い合わせ先: otuki.3104@gmail.com

**実装のポイント**:
- セクション分けで読みやすく
- お問い合わせフォームから飛べるようリンク設置
- 制定日を明記

---

**法務ページ共通の実装仕様**:
- 共通ヘッダー・フッターを使用
- Tailwind CSSで統一されたデザイン
- モバイル対応
- トップページへ戻るリンクを配置
- 制定日・改定日を記載

---

## 備考

### 製品固有の情報
- **製品名**: Lucid-SRD
- **価格**: シングルライセンス ¥400,000、サイトライセンス ¥1,200,000（税込）
- **対応ディスプレイ**: Sony Spatial Reality Display (ELF-SR2)
- **対応ファイル形式**: STL, OBJ, DICOM
- **特典**: ダウンロード版にはジェスチャーコントロールアプリ（¥20,000相当）同梱

### 実装時の注意事項
- プレースホルダー画像は後で実際の製品画像・スクリーンショットに差し替え
- ロゴファイルは assets/images/ に配置
- お問い合わせフォームの送信機能は後で実装（Netlify Forms推奨）
- 体験版は問い合わせ後に提供する形式（自動DLは不要）
- 運営責任者名は特定商取引法ページで要確認・追記

### 今後の拡張予定
- 実際の製品画像・動画の追加
- 活用事例の詳細な説明文
- ユーザーの声・導入事例
- ブログ機能（SEO強化）
- 決済システムの統合

---

**このドキュメントは開発の指針となる仕様書です。実装時はこのドキュメントを参照しながら、段階的に機能を追加してください。**

**Claude Codeでの実装開始コマンド例**:
```
CLAUDECODE.mdの仕様に従って、Lucid-SRDの販売サイトを作成してください。
まずはindex.htmlから開始し、フェーズ1の基本構造を実装してください。
```