# renovate

imagica-et 共通の Renovate 設定（preset）。

## usage

```json
{
  "extends": ["github>imagica-et/renovate"]
}
```

## default（`default.json`）の方針

- `config:recommended` ベース、タイムゾーン Asia/Tokyo
- PR 作成は **毎週月曜 9 時前**。lockfile メンテナンスは毎月 1 日
- **公開から 3 日経った版のみ採用**（`minimumReleaseAge: 3 days` / `internalChecksFilter: strict`）。リリース日時を返さないデータソース（Docker イメージ等）は待たずに通す
- **メジャーと 0.x 系の minor は Dependency Dashboard 承認制**。Dashboard でチェックを入れたものだけ PR 化される
- devDependencies の minor/patch は 1 本にまとめる（lockfile のみ更新）。linters もまとめる
- **自動マージは既定で行わない**。main マージがデプロイを起動するリポジトリがあるため、必要なリポジトリ側で明示的に有効化する。例:

```json
{
  "extends": ["github>imagica-et/renovate"],
  "packageRules": [
    {
      "matchDepTypes": ["devDependencies"],
      "matchUpdateTypes": ["minor", "patch"],
      "automerge": true
    }
  ]
}
```

## 任意の preset

### `group-non-major`

minor/patch を依存種別に関係なく 1 本の PR にまとめる（CI が重いリポジトリ向け）。0.x の minor は承認制のままグループから外れる。

```json
{
  "extends": ["github>imagica-et/renovate", "github>imagica-et/renovate:group-non-major"]
}
```

## 変更時の検証

```sh
npx --package renovate -- renovate-config-validator --strict default.json group-non-major.json
```
