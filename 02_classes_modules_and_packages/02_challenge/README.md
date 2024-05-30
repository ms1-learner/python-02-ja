# チャレンジ2
自動車販売システムの作成

## パート1
- Vehicleクラスの定義
  - 独立したモジュールに `Vehicle` クラスを作成します。属性として、車種 (model)、メーカー (make)、年式 (year)、価格 (price)、割引額 (discount) を用意します。これらの属性を設定するメソッドと取得するメソッドも用意します。
- 車両の在庫
  - `Vehicle` インスタンスのコレクションを管理する `Inventory` クラスを作成します。さまざまな条件 （車種、年式、価格帯など） にもとづいて、車両を追加したり取得したりするメソッドを実装します。
- 割引の適用
  - 車両に割引を適用するメソッドを `Inventory` クラスに実装します。リスト内包表記、ラムダ関数、デコレーターのいずれかを使用するか、これらを組み合わせて、動的な割引基準に対応します （例： SUV全車5%オフ）。
- 検索機能
  - 正規表現を使用して、車種で車両を検索するメソッドを追加します。このメソッドでは、検索パターンに一致する車両のリストを返してください。
- 車両の反復
  - `Inventory` クラスにジェネレータを実装し、すべての車両を反復処理して一度に1台の車両を引き渡すようにします。

## パート2
- 車両データの解析
  - テキストファイルから車両データを解析するモジュールを作成します (車両の詳細情報を記載したサンプルファイルを提供してください)。文字列整形とファイル操作を使用し、このデータを読み込んで処理します。
- 車両インスタンスの作成
  - 解析したデータを使用して `Vehicle` のインスタンスを作成し、それを `Inventory` に追加します。

## 例

**vehicles.txt**
```
Corolla,Toyota,2020,20000
Civic,Honda,2021,22000
```

**main.py**
```python
from inventory import Inventory
from data_parser import parse_vehicle_data

vehicles = parse_vehicle_data("vehicles.txt")
inventory = Inventory()
for vehicle in vehicles:
    inventory.add_vehicle(vehicle)

print(inventory.vehicles[0].get_model())  # Corolla
print(inventory.vehicles[0].get_make())  # Toyota
print(inventory.vehicles[0].get_year())  # 2020
print(inventory.vehicles[0].get_price())  # 20000
print(inventory.vehicles[0].get_discount())  # 0

inventory.apply_discount(lambda v: v.make == "Toyota", 5)
toyotas = inventory.search_vehicles("Corolla")

for toyota in toyotas:
    toyota.display()

for vehicle in inventory.retrieve_vehicles():
    vehicle.display()
```
