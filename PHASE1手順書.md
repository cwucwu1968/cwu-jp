# フェーズ1手順書 — リポジトリ作成から Pages 連携・実証まで

対象：makabe／連合会側の作業と、Muse の作業の分担を書いたもの。
前提：Cloudflare アカウントと GitHub アカウントは連合会管理メールで作成済み（2026-11-25）。

## 1. GitHub リポジトリを作る（連合会側、約5分）

1. GitHub に連合会アカウントでログインする。
2. New repository を作る。名前の案：`cwu-jp`（決まっていなければこれでよい）。
3. Public か Private か：サイト原本は公開サイトの元になるので Public でよい。迷う場合は Private で作り、Pages 連携時に必要なら変更する。
4. このパッケージのファイル（`index.html`、`_redirects`、`README.md`、この手順書）をアップロードする。`Add file` → `Upload files` でよい。
5. リポジトリの URL を Muse に教える。例：`https://github.com/<連合会アカウント>/cwu-jp`

## 2. Cloudflare Pages プロジェクトを作る（連合会側、約10分）

重要：最初から GitHub 連携方式で作ること。直接アップロードで作ると、後から Git 連携に切り替えられない。

1. Cloudflare ダッシュボード → Workers & Pages → Create → Pages → Connect to Git。
2. GitHub アカウントを連携し、手順1のリポジトリを選ぶ。
3. プロジェクト名の案：`cwu-jp`。
4. Framework preset：None（静的サイト）。Build command：なし。Build output directory：空欄（ルート）。
5. Save and Deploy を押す。仮アドレス（`https://cwu-jp.pages.dev` のような形）が発行される。
6. 仮アドレスを Muse に教える。

## 3. Muse が確認すること（Muse、仮アドレスのみ）

- 仮アドレスでトップが表示されること、9セクションの切り替え、モバイルメニュー、スマホでの横はみ出しがないこと。
- リンク切れがないこと（PDF・動画・写真は現行サイトへのリンクのまま）。
- コンソールエラーがないこと。

## 4. 更新操作4種の実証（Muse＋makabe）

次の順で、すべてプレビュー→makabe 確認→公開のフローで回す。

1. 記事の追加（例：更新情報に1件追加）
2. PDF の差し替え（例：差し替え用 PDF を1件）
3. 既存記事の修正（例：文言の修正）
4. 変更の取り消し（巻き戻し、Git の revert／以前のデプロイへのロールバック）

各操作のたびに、プレビューの URL を makabe に見せ、確認を得てから本番（といってもこの段階では pages.dev の仮サイト）に反映し、表示を確認して報告する。

## 5. Muse に直接作業させる場合

- パスワードや API トークンをチャットに貼らないこと。
- 方法は次のどちらか：
  - （a）makabe がブラウザで GitHub／Cloudflare にログインした状態で、Muse にブラウザ作業を任せる。
  - （b）GitHub リポジトリに Muse 用のアカウントを collaborator として招待する（権限は必要最小限）。
- どちらにするかは makabe が決める。決まるまでは、上記の手順1・2を連合会側で行い、Muse は仮アドレスの確認と更新実証の準備だけを行う。

## やらないこと（このフェーズでは）

- www.cwu.jp や cwu.jp の DNS 変更、Cloudflare への本番ドメイン接続はしない。
- Wix サイトへの変更はしない。
- メール（MX・TXT・DKIM）に関わる設定変更はしない。
