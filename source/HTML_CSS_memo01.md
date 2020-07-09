# HTML/CSS
HTML  
```
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <link rel="stylesheet" href="assets/css/step05.css">
    <title>KROWL MAGAZINE sample</title>
  </head>
  <body>
    <header class="page-header">
      ヘッダー
    </header>
    <main class="main-content">
      メインコンテンツ
      <div class="main-visual">
        メインビジュアル
      </div>
      <section class="intro-section">
        イントロセクション
        <div class="intro-section__header section-header">
          セクションの始まり
        </div>
        <nav class="intro-section__nav">
          ナビゲーション
        </nav>
        <div class="intro-section__content">
          コンテンツ
        </div>
        <div class="intro-section__contact">
          <!-- 上記のintro-section__contactは周りの白い余白を含めた要素 -->
          <div class="contact-block">
            お問い合わせ
          </div>
        </div>
      </section>
    </main>
    <footer class="page-footer">
      フッター
    </footer>
  </body>
</html>
```
  
CSS
```
/* 全体のスタイル */
html,
body {
  font-size: 1.8rem;
  text-align: center;
}

/* １番大きな要素 */
.page-header,
.page-footer,
.main-content {
  margin: 30px 0;
  border: 5px solid red;
}

/* main-content内の要素 */
.main-visual,
.intro-section {
  margin: 30px;
  border: 5px solid green;
}

/*  intro-section内の要素 */
.intro-section__header,
.intro-section__nav,
.intro-section__content,
.intro-section__contact {
  margin: 30px;
  border: 5px solid blue;
}
```
  
CSS2
```
/* 横並び */
.page-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* 横並び */
.page-header__info {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* 縦並び */
.page-header-info__txt span {
  display: block;
}
```
  

