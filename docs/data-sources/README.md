# 公開データ源カタログ (AWAI-2944)

親: [AWAI-706](https://linear.app/kotobalabs/issue/AWAI-706) /
子: [AWAI-2944](https://linear.app/kotobalabs/issue/AWAI-2944)。
機械可読の目録は [catalog.edn](./catalog.edn)。

実データの repo 取込はしない (G7)。公開集計の典拠目録と
operator 取込契約の文書のみ。個人データなし (G2)、assessment-only (G5)。
連絡・申請・個人情報収集は行っていない。

## 即時利用可

- 環境省花粉飛散量調査年報 (PDL1.0): 地点シーズン総飛散数→年次 emission-density。
- 東京都オープンデータ花粉情報 (CC-BY-4.0): ベースライン参照 (2017年時点)。

他は閲覧専用扱い (都navi・tenki・ポールンロボ・はなこ条件未確認)。

## 単位系の注意

はなこは個/m3 (体積法)、都県・環境省年次は個/cm2 (ダーラム系)。
emission-density の単位・粒度定義は未確定で、換算ルール確定前の混用はしない。

## 分析拡張 4件

1. 都道府県×樹種クラス集計アダプタ: 公開集計→aggregate stand 行で burden 校正。
2. シーズンnowcast包絡: 地域週平均で dynamics の rate を包絡束縛。
3. 苗木・再造林需給校正: 公開需給で supply/consent-rate envelope を典拠付け。
4. 保護・同意・炭素制約レイヤ: 公開割合→決定論的丸めで代表値付与。

いずれも repo 外 operator script が intake し、repo には集計・bool/enum・典拠のみ。
ID は `aggregate:<地域クラス>:<樹種クラス>:<年度>` 形式に限る。

## 未解決

一次資料の表番号・スキーマ版固定、はなこ等の利用条件原文、
emission-density 定義、ie-flow I/F、取込配置主体、beat 注入 I/F、
丸め粒度下限の数値基準。取込実装前に典拠を固定する。
