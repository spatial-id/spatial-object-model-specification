# Spatial Object Model （仕様のドラフト）

## SOM (Spatial Object Model) Core

空間オブジェクトは以下のようなインターフェスをもつこと。

```
interface SOM {
  id                 ID;
  center             An array of the lnglat;
  resolution:        The zoom level;
  afxy:              The ZFXY.
}
```

### コンストラクタ

* 空間ID、緯度経度及び高度、ZFXYのいずれかを引数として受け取り空間オブジェクトを返す。

## Methods

### Space.getSpaceById()

* ID を引数として受け取り空間オブジェクトを返す。

### Space.getSpaceByLocation()

* 緯度経度及び高度を引数として受け取り空間オブジェクトを返す。

### Space.getSPaceByZFXY()

* ZFXY を引数として受け取り空間オブジェクトを返す。

### .up()

![up](https://user-images.githubusercontent.com/309946/168220328-47e09300-c4dc-4ad1-adae-2cb17aff23ab.png)

* パラメータがない場合は、現在の空間オブジェクトのひとつ上の空間オブジェクトを返す。
* パラメータが指定されている場合は、その個数分の空間オブジェクトを配列で返す(？)
* マイナスも受け付けられるといい。
* メートルで指定できるといいかも(？)

### .down()

![down](https://user-images.githubusercontent.com/309946/168220818-f89a73b1-b99c-462d-9fcb-5eae0eac03eb.png)

* パラメータがない場合は現在の空間オブジェクトのひとつ下の空間オブジェクトを返す。
* パラメータが指定されている場合は、その個数分の空間オブジェクトを配列で返す(？)
* マイナスも受け付けられるといい。
* メートルで指定できるといいかも(？)

### .north(), .east(), south(), .west()

![north](https://user-images.githubusercontent.com/309946/168221234-b03809ef-6c69-442b-98d3-583b4391108e.png)

* パラメータがない場合は、現在の空間オブジェクトの隣のオブジェクトを返す。
* パラメータが指定されている場合は、その個数分の空間オブジェクトを配列で返す(？)
* マイナスも受け付けられるといい。
* メートルで指定できるといいかも(？)

### .surroundings()

![surroundings](https://user-images.githubusercontent.com/309946/168221371-b1ec30c7-f501-4a6b-ad64-5a6345fb9665.png)

* 現在の空間オブジェクトのまわりにあるすべての空間オブジェクトを配列で返す。

### .parent()

* 現在の空間オブジェクトから、分解能（ズームレベル）を一つ下げて、その空間オブジェクトを返す。

### .children()

* 現在の空間オブジェクトから、分解能（ズームレベル）を一つ上げて、そこに含まれるすべての空間オブジェクトを返す。

### .contains()

* 指定された緯度経度が、指定されたボクセル内に含まれるかどうかを判定して bool 値を返す。


## 参考: NodeJS ベースの SDK （があると仮定して）での実装例

```node
const space = new Space(12345678) // 空間ID、緯度経度及び高度、ZFXYのいずれか

// 南へ一つ、上へひとつ、東へひとつ移動したあとで、そこにスカイツリーの頂上があるかどうかを判定する。
const result = space.south().up().east().contains(139.81088744999997, 35.71027146141545, 634)
```
