# 花粉データ基盤の一本化 (AWAI-2941)

親: [AWAI-706](https://linear.app/kotobalabs/issue/AWAI-706) /
子: [AWAI-2941](https://linear.app/kotobalabs/issue/AWAI-2941)。

正本は1つにし、形式は増やさない。**forest CARv2** を単一正本とし、
10形式は CID からの派生 projection として query する。
機械可読の対応表は [unified-base.edn](./unified-base.edn)。

## 正本 (forest)

`forest` は Filecoin Forest の `.forest.car.zst` である。
複数 CAR block を 8KiB zstd frames に包み、index を skippable zstd frame に置く。
正規の生成・検証は `forest-tool snapshot compress` / `validate`。
inner CAR は awai の CARv2 (Forest 互換の表明はしない)。
参考実測: seed-CAR 5277 B → zstd 1572 B (29.8%、zstd 1.5.7、plain zstd で frame/index 構造ではない)。
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
