常設型トラフィックカウンターおよび CCTV 映像を活用した AI 型トラフィックカウンターで観測された、全国の方向別交通量データを取得する。

実体は GeoServer の WFS 2.0.0 `GetFeature` であり、エンドポイントは 1 本のみ。取得する様式（データ種別）は `typeNames` の値で切り替える。

## 様式（typeNames）

| 様式  | typeNames                       | 観測機器     | 集計単位    | 検索可能期間 |
| ----- | ------------------------------- | ------------ | ----------- | ------------ |
| 様式1 | `t_travospublic_measure_5m`     | 常設トラカン | 5分間交通量 | 過去1か月分  |
| 様式2 | `t_travospublic_measure_1h`     | 常設トラカン | 1時間交通量 | 過去3か月分  |
| 様式3 | `t_travospublic_measure_5m_img` | CCTVトラカン | 5分間交通量 | 過去1か月分  |
| 様式4 | `t_travospublic_measure_1h_img` | CCTVトラカン | 1時間交通量 | 過去3か月分  |

`features[].properties` の項目は様式により異なる。様式 1・2 はループ／超音波などの機器状態フラグを、様式 3・4 はカメラや映像解析に関する状態フラグを持つ。

## リクエスト例

```
https://api.jartic-open-traffic.org/geoserver?service=WFS&version=2.0.0&request=GetFeature&typeNames=t_travospublic_measure_5m&srsName=EPSG:4326&outputFormat=application/json&exceptions=application/json&cql_filter=道路種別=3 AND 時間コード=202502100900 AND BBOX(ジオメトリ,139.15,35.141,139.32,35.56,'EPSG:4326')
```

## 注意事項

- 各種トラカンは観測条件により精度が大きく変動する場合がある。本データには気象状況等の環境要因や機器故障等により正確でないデータが含まれることがあり、国土交通省による正式な交通量の調査結果ではない。職員によるデータチェックは実施していない。
- 近畿地方整備局の管轄エリアにおける CCTV トラカンの観測値は、システム上の都合により当面は様式 3（5 分間交通量）のみの提供となる。
- 本 API の利用には「交通量 API 利用規約」への事前同意が必要。
