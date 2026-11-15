# 花粉分析の統合 (AWAI-2939、AWAI-2948)

20分析に加え、loop-dominance (優勢ループ) と sensitivity-mc (感度分布) を
`dynamics.kotoba` 基盤に追加登録した (計22件)。いずれも operator 実行の
candidate-only である。

親: [AWAI-706](https://linear.app/kotobalabs/issue/AWAI-706) /
子: [AWAI-2939](https://linear.app/kotobalabs/issue/AWAI-2939) /
project: `cloud-itonami/actor-kafun`。
関連: [AWAI-928](https://linear.app/kotobalabs/issue/AWAI-928) (bokumetsu)、
[AWAI-2928](https://linear.app/kotobalabs/issue/AWAI-2928) (sugi 協力・同意ルール)。

repo 正本は `cloud-itonami/app-itonami-kafun` に集約する
(`actor-kafun` は同 repo への redirect)。

## 層構造

オントロジーが静的意味層、動態モデルが時間・確率層、ledger が証拠層。

- 意味: `schema/ontology.kafun.edn` (`:stand` の12属性・verdict 6種・unrepresentable 4件)
- 動態: `dynamics.kotoba` (readiness stock-flow)、`react_loop.kotoba` (ReAct beat)、
  `remediate.kotoba` (verdict gate)
- 証拠: `data/persisted/kafun.remediation.kotoba.edn` (append-only、gitignored)

機械可読の対応表は [registry.edn](./registry.edn)。20件すべて
assessment-only (G5)、合成 seed (G7)、個人データなし (G2)。

## awaifs 契約

`awai-fs-readiness-v1` の exclusions により research/documentation は
受入対象外。本ディレクトリは candidate-only で gate 証拠に流用しない。
データは repo 内 `data/` に宣言し、将来の観測は dated evidence で
readiness 台帳に登録する (baseline 変更時は新旧対応表が必須)。

## ゲート遵守

G1 (撲滅=restoration)・G4 (carbon) の拒否は forecast 経路でも迂回しない
(`step-system` は同一 `remediate/verdict` を再評価するのみ)。
対外の協力活動は AWAI-2928 の10則 (同意が先・下書きまで・公開は人承認) に従う。
