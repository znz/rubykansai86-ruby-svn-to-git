# Ruby svn to git

author
:   Kazuhiro NISHIYAMA

content-source
:   第86回 Ruby関西 勉強会

date
:   2019/05/11

institution
:   株式会社Ruby開発

allotted-time
:   20m

theme
:   lightning-simple

# 自己紹介

- 西山 和広
- Ruby のコミッター
- twitter, github など: @znz
- 株式会社Ruby開発 www.ruby-dev.jp

# svn から git へ

- 参考:
  令和時代のRubyコア開発 - k0kubun's blog
  <https://k0kubun.hatenablog.com/entry/ruby-core-2019>
- Ruby のコア開発が Subversion から Git に移行

# 歴史

- バージョン管理システム以前
  - news (nntp) とかメーリングリスト (ML) とか
- CVS : ruby-cvs ML の名前の由来
- Subversion : 安定版のメンテナンスはまだこちら
- Git : 開発版はこちら (安定版も 2.7 から)

# 歴史 (CVS → Subversion)

- 連携しているものもほぼない時代
- すんなり移行
- ruby-cvs ML の名前はそのまま
  - svn → git の時は特に話題になることもなく同様にそのままに

# 歴史 (Subversion → ?)

- svk を手元で使っている人もいた
- Mercurial などには移行せず
- Git が主流に
- svn も git-svn 経由で使う人が増えた

# なぜ移行?

- バージョン管理システムの主流が Git
- git-svn を使っている人が多かったが色々と面倒だった
- GitHub で貢献者が出なかった
  (Co-authored-by も git-svn が挟まるとダメだった)

# GitHub ではなく cgit

- プロプライエタリなものは使わないポリシーの人 (Eric Wong) がいた
- 独自 hook の都合でいきなり GitHub 移行は大変そうだった

# Git化に必要だった作業達

- コミットフックの Git 対応
- Ruby リポジトリ内の tool/* スクリプト
- 公式の issue tracker の Redmine
- RubyCI や ci.rvm.jp などの CI や bot
- cgit の用意、運用、アナウンス

# GitHub で運用している他プロジェクトとの違い

- GitHub 上でのマージボタンは使わない
  - 同期が一方向のため
- 開発版ブランチが trunk (master ではない)
  - これも変更すると影響があるので変えるならまた別途

# 制限事項

- `git push -f` は禁止
- trunk 以外へのブランチへの push は禁止
  (安定版ブランチはまだ svn からのミラー)
- マージコミットはしない
  - 移行直後に1個入れてみたらいくつか懸念点があったので当面は使わない

# よかったこと

- git-svn の複雑さに悩まなくてよくなった
- git.ruby-lang.org が日本からだと github.com より速い
- <https://github.com/ruby/ruby/graphs/contributors> に貢献者がのるようになった

# GitHub はミラー

- GitHub は Subversion 時代と変わらずミラー
- cgit とずれて push -f されることもある
  - 手元のがおかしくなったら「`git fetch -f`」とか「`git checkout -B trunk origin/trunk`」とか clone し直しとか

# GitHub

- pull request も可能
  - GitHub 上でのマージはしないが、コミッターがマージして push できる
- 議論が必要なものは bugs.ruby-lang.org のチケットで

# まとめ

- Ruby 本体のレポジトリは Subversion から Git に
- 安定版は次の 2.7 から
- 連携ツールもほぼ移行完了
- GitHub はミラーだが pull request も可能
