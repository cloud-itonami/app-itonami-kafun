# 花粉データ基盤の一本化 (AWAI-2941)

親: [AWAI-706](https://linear.app/kotobalabs/issue/AWAI-706) /
子: [AWAI-2941](https://linear.app/kotobalabs/issue/AWAI-2941)。

正本は1つにし、形式は増やさない。**forest CARv2** を単一正本とし、
10形式は CID からの派生 projection として query する。
機械可読の対応表は [unified-base.edn](./unified-base.edn)。

## 正本 (forest)

`forest` は CID-block の集合とその closure を指す本書の定義である。
apex 文書に forest の語はなく、命名の固定はしない。
P0 route に従う: Form → canonical bytes → CID → pack。

- 意味共有: Kotoba S-form。物理表現の統一を意味しない。
- 値・検証: `kotoba.value.v1`、tag-42 と canonical re-encode match。
- 移動: CARv2/index/trustless。bytes 面は Yataverse raw-only。
- 束ね: Kotobase signed commit / authorized query / causal commit。

典拠は `network-awai-apex` の storage architecture と P0 baseline、
受入は `awai-fs-readiness-v1`。

## 派生 (projection)

EDN・JSON・CSV・SQLite・Parquet・GeoJSON・TopoJSON・JSON-LD・EAVT・CAR raw は
いずれも CID から再生成できる派生であり、正本にしない。
query 入口は FILE・QUERY (Datalog/authorized query)・LAKE (SQL/Parquet) の3種。

## 境界

pack locality と node adapter は P1/new scope で対象外。
kafun 側の採用は candidate-only (readiness の research 除外に従う)。
G1-G8・N1-N5・同意10則、Native/Otehon 境界を維持する。
