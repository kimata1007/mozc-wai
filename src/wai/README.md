# `wai/` — WritingAssistantIME 用の集約 Bazel package

このディレクトリは [WritingAssistantIME](https://github.com/<owner>/WritingAssistantIME) から参照される `libmozc_wai.a` を作るための fork 専用 package。

## 設計書

`<owner>/WritingAssistantIME` の `docs/design-doc/202605-006_mozc-integration/README.md` §2.5 を参照。

## なぜ別 fork repo にあるのか

WritingAssistantIME 本体のリポジトリには Bazel を入れたくない（OSS 利用者に Bazel install を強いると離脱率が高い）。その代わり fork で `.a` + 辞書を pre-build → GitHub Releases に upload → 本体側は `download_artifact.sh` で取得する設計。詳細は設計書 §2.5.1。

## upstream merge 手順

```sh
git fetch upstream
git checkout wai/build-and-release
git merge upstream/master
# 競合なし → 新 tag を打って Release を作る
git tag v0.1.x
git push origin v0.1.x
```

`wai/` は upstream に存在しないため、構造上 merge 競合は起きない。
