# jartic-open-traffic-openapi

国土交通省交通量 API（JARTIC が提供する交通量データのオープン化 API）の非公式 OpenAPI 定義。

常設型トラフィックカウンターおよび CCTV 映像を活用した AI 型トラフィックカウンターで観測された、全国の方向別交通量データを取得する API を記述する。実体は GeoServer の WFS 2.0.0 `GetFeature` であり、エンドポイントは 1 本のみ。取得する様式（データ種別）は `typeNames` の値で切り替える。

## 様式

| 様式  | typeNames                       | 観測機器     | 集計単位    | 検索可能期間 |
| ----- | ------------------------------- | ------------ | ----------- | ------------ |
| 様式1 | `t_travospublic_measure_5m`     | 常設トラカン | 5分間交通量 | 過去1か月分  |
| 様式2 | `t_travospublic_measure_1h`     | 常設トラカン | 1時間交通量 | 過去3か月分  |
| 様式3 | `t_travospublic_measure_5m_img` | CCTVトラカン | 5分間交通量 | 過去1か月分  |
| 様式4 | `t_travospublic_measure_1h_img` | CCTVトラカン | 1時間交通量 | 過去3か月分  |

## 出典

- ガイダンスサイト: <https://www.jartic-open-traffic.org/>
- 交通量 API 仕様書（API リクエストの作成方法）令和 8 年 1 月版
- 交通量データ利用の手引き令和 7 年 5 月版

## 留意事項

- この定義は上記の公開資料を基に作成した非公式のものであり、国土交通省・JARTIC が公開・保証するものではない。
- `cql_filter` は CQL 文字列であり、OpenAPI の型では内部文法（道路種別・時間コード・BBOX）を強制できない。`getFeature` の説明および例を参照すること。
- 仕様書の API 概要表には「認証方式有」と記載があるが、リクエストに認証情報を渡すパラメータの記載がなく、例示 URL も無認証であるため、本定義では `securitySchemes` を定義していない。
- `outputFormat` は `application/json`（GeoJSON）と `csv` を取り得るが、本定義ではレスポンスを GeoJSON のみ記述する。
- 提供されるデータは正式な交通量の調査結果ではなく、精度が変動する場合がある。利用には「交通量 API 利用規約」への事前同意が必要。
