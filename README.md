# Swift コーディング規約
## 基本仕様
* [Swift6.2の構文に対応している](https://docs.swift.org/swift-book/documentation/the-swift-programming-language)
* **[MUST]** [Swift API Design Guideline](https://www.swift.org/documentation/api-design-guidelines/#naming) に従うこと

## 命名
### 共通事項
- **[MUST]** 非 ASCII 文字を名前に使用しないこと
- **[MUST]** 意味のある名前を付けること
- **[MUST]** 省略形を避けること
     * 必要以上に短縮せず、可読性を優先する
 
### ファイル名
- **[SHOULD]** class名, protocol名, と一致させること
     - ただし、関連が分かりやすくなる場合はこの限りではない
- **[MUST]** extension クラスは元 class名+extension とすること
    - ex) `MyClass+Extension.swift`

### 変数・定数・プロパティ名／関数名
- **[MUST]** lowerCamelCaseを使用すること
     * Swiftでは変数・定数ともにlowerCamelCaseを使用します。
```swift
    let maxRetryCount = 3
    var currentIndex = 0
```

- **[MUST]** 定数の命名も変数に従うこと
  - UpperCamelCase、SNAKE_CASE を用いたりしてはならない
  
- **[MUST]** 非 ASCII 文字を名前に使用しないこと

- **[MUST]** 意味のある名前を付けること
     * 変数や定数が何を表しているのかを明確にする。
```swift
    let userAge = 25
    var isLoggedIn = false
```

- **[MUST]** 省略形を避けること
     * 必要以上に短縮せず、可読性を優先する。
```swift
// Bad
let usrAg = 25

// Good
let userAge = 25
```

- **[MUST]** 文脈に応じた名前を付けること
     * 変数が使われる場所や用途に応じて適切な名前を選ぶ。
```swift
// Bad
let data = "John"

// Good
let userName = "John"
```

- **[MUST]** 定数には名詞、変数には状態を表す動詞を含める
     * 定数は名詞、変数は動詞を含む名前にする。
```swift
let maxConnections = 10
var updateCount = 0
```

- **[MUST]** ブール値には肯定的な名前を付ける
     * `is`や`has`などを使い、真偽が明確になるようにする。
```swift
var isUserLoggedIn = true
let hasPermission = false
```

- **[MUST]** 単数形・複数形を正しく使うこと
     * 配列やコレクションには複数形を使う。
```swift
let userNames = ["Alice", "Bob"]
let userName = "Charlie"
```
- **[MUST]** 不要なプレフィックスを避ける
     * `k`や`m`などのプレフィックスは使わない。
```swift
// Bad
let kMaxRetryCount = 3

// Good
let maxRetryCount = 3
```
- **[MUST]** 短すぎる名前を避けること
     * `x`, `y`のような短い名前は、特別な意味がある場合を除き避ける。
     * `hoge` や `foo`, `fuga` のような意味のない名前は避ける。

- **[MUST]** ベンダープレフィックスを付与しないこと
  - ただし、`NSObject`の継承や既存クラスの extension などを用いて Objective-C からも利用可能になる場合は付けること
  
- **[SHOULD]** 階層構造を示す命名は避け、ネストで表現すること

```swift
// Good
class Recipe {
    enum Type {
        case none
    }
}

```

- **[MUST]** UI部品は末尾にその部品であることが容易にわかるように命名すること
```swift
// Bad
let title: UILabel
let cancel: UIButton

// Good
let titleLabel: String
let cancelButton: UIButton
```

- **[MUST]** UI部品はその部品が何の部品か容易にわかるように命名すること
```swift
// Bad
let label: UILabel
let button: UIButton

// Good
let titleLabel: String
let cancelButton: UIButton
```

### 型・プロトコル名
- **[MUST]** UpperCamelCase（パスカルケース） を使います。
```swift
// Bad
class landmarkList {}

// Good
class LandmarkList {}
```

- **[SHOULD]** プロトコル名はなるべく「〜Delegate」「〜able」「〜ing」で終わること
```swift
// Good
protocol Animating {}

```

### Enum
- **[MUST]** UpperCamelCase（パスカルケース） を使います。
```swift
// Bad
enum direction {
      case north
      case south
}

// Good
enum Direction {
      case north
      case south
}
```
- **[MUST]** 値は lowerCamelCase で命名すること
```swift
// Bad
enum Direction {
      case North
      case South
}

// Good
enum Direction {
      case north
      case south
}
```

## コーディング
### 共通事項
- **[SHOULD]** 可能な限り、ドキュメントコメントを書くこと
- **[MUST]** 不要なスペースなどは削除すること
- **[MUST]** 型の指定では、常にコロンを識別子の後ろに繋げる
     * 識別子に型を指定する時は、常に識別子のすぐ後ろにコロンを置き、空白を一つあけて型名を書きましょう。
```swift
// Good
class SmallBatchSustainableFairtrade: Coffee { ... }

let timeToCoffee: NSTimeInterval = 2

func makeCoffee(type: CoffeeType) -> Coffee { ... }
```

- **[MUST]** ディクショナリの型定義をするときも、常にキーの型のすぐ後にコロンをおいて、空白の後に値の型を指定します。

```swift
// Good
let capitals: [Country: City] = [ Sweden: Stockholm ]
```
- **[MUST]** 将来的に廃止が予定されている構文を使わないこと
- **[MUST]** 行末に`;`を付けないこと
- **[MUST]** `self` は省略することただし、インスタンス時やクロージャー内など省略できないところはこの限りではない
     * `self`の持つプロパティやメソッドへアクセスする時、デフォルトでは`self`への参照は省きましょう。
     * 明示的に`self`を入れるのは言語によって必要と判断された場合だけにしましょう-たとえばクロージャ内、もしくはパラメータ名の衝突がある場合などです。

```swift
// Good
private class History {
    var events: [Event]

    func rewrite() {
        events = []
    }
}

extension History {
    init(events: [Event]) {
        self.events = events
    }

    var whenVictorious: () -> () {
        return {
            self.rewrite()
        }
    }
}
```

### 空白
- **[MUST]** インデントにはソフトタブを使い、幅は 4 スペースにすること
- **[MUST]** ファイル終端は改行する
- **[MUST]** コードをロジック毎に分割するために、空白行を惜しみなく使う
- **[MUST]** 行末に空白を残さない
- **[MUST]** オープンブラケットは同じ行に記述すること
```swift
// Good
func update() {
}
```
### オペレータ定義では空白を使う
- **[MUST]** オペレータを定義するときは、オペレータの前後に空白を使いましょう。  
```swift
// Bad
func <|(lhs: Int, rhs: Int) -> Int
func <|<<A>(lhs: A, rhs: A) -> A

// Good
func <| (lhs: Int, rhs: Int) -> Int
func <|< <A>(lhs: A, rhs: A) -> A
```

### 変数・定数・プロパティ
- **[MUST]** グローバル変数として定義しないこと
- **[MUST]** 利用しない戻り値、引数は`_`にすること
- **[MUST]** 可能な限り`var`宣言よりも`let`宣言を使う
- **[SHOULD]** 可能な場合は型宣言を省略すること。ただし、型推論がコンパイル速度に影響を及ぼす場合はその限りではない
- **[MUST]** 最もスコープが狭くなるようにアクセスレベルを設定すること
- **[MUST]** 外部から読み込めるが、書き込ませたくないプロパティには`private(set)`を明示すること
- **[MUST]** プロパティの属性として`weak`を使える場所では使うこと
  - `@IBOutlet`やデリゲートなど、循環参照が発生しうる箇所に付与すること

```swift
// Good
weak var delegate: FooDelegate
@IBOutlet weak var textLabel: UILabel!
```

- **[MUST]** Computed Property について、省略可能なとき`get`を省略すること

```swift
// Good
var foodCount: Int {
    return foods.count
}
```

- **[SHOULD]** 副作用を伴う場合、`willSet`, `didSet`に記述すること

### 関数
- **[MUST]** 第一引数を省略しない。ただし、引数が1つで省略した方が自然に理解できる関数名の場合はこの限りではない。
```swift
// Bad
func send(_ message: String, to user: User)
// Good
func send(message: String, to user: User)
```

- **[MUST]** 引数の記載が省略できる場合は省略する
```swift
// Good
func doSomething() -> Void {
}

// Bad
func doSomething() {
}
```

- **[MUST]** 実行を継続するには基準を満たす必要があるような場合は、なるべく早期にコードブロックから抜け出すようにしましょう。
```swift
// Bad
if n.isNumber {
    // Use n here
} else {
    return
}

// Good
guard n.isNumber else {
    return
}
// Use n here
```

- **[MUST]** 可能であれば `guard`を使い、早めにコードブロックから抜け出すようにしましょう。


### Enum
- **[MUST]** 型名が省略可能なときは省略すること
```swift
// Good
user.status = .guest
```

- **[MUST]** undefined などの想定していない値の定義はしない。ただし、エラー定義の場合はこの限りではない

```swift
// Bad
enum Direction {
      case north
      case south
      case undefined
}

// Good
enum Direction {
      case north
      case south
}

// Good
enum DirectionError: Error {
      case noItem
      case undefined
}
```

### クラス・構造体
- **[MUST]** Objective-C からの参照が必要な場合を除き`NSObject`を継承しないこと
- **[SHOULD]**  クラスより構造体を使うようにする
     * クラスでしか提供できない機能（同一性やデイニシャライザなど）を必要としない限り、クラスではなく構造体で実装しましょう。
     * 継承は通常、クラスを使う主な良い理由にはなりません。なぜなら、多様性はプロトコルによって実現可能であり、実装の再利用はコンポジションによって実現可能であるからです。

```swift
// BAD
class Vehicle {
    let numberOfWheels: Int

    init(numberOfWheels: Int) {
        self.numberOfWheels = numberOfWheels
    }

    func maximumTotalTirePressure(pressurePerWheel: Float) -> Float {
        return pressurePerWheel * Float(numberOfWheels)
    }
}

class Bicycle: Vehicle {
    init() {
        super.init(numberOfWheels: 2)
    }
}

class Car: Vehicle {
    init() {
        super.init(numberOfWheels: 4)
    }
}
```


```swift
// Good
protocol Vehicle {
    var numberOfWheels: Int { get }
}

func maximumTotalTirePressure(vehicle: Vehicle, pressurePerWheel: Float) -> Float {
    return pressurePerWheel * Float(vehicle.numberOfWheels)
}

struct Bicycle: Vehicle {
    let numberOfWheels = 2
}

struct Car: Vehicle {
    let numberOfWheels = 4
}
```
- **[MUST]**  デフォルトでクラスを`final`にする
     * クラスは初めは`final`にしておき、継承の正当な必要性が確認された場合にサブクラス化を許容する目的でのみ変更するべきです。さらにその場合、クラス内のそれぞれのクラスも、可能な限り同じルールに則り、同じように`final`を適用します。

- **[MUST]** 可能な限り型パラメータは省く
     * パラメータ化された型のメソッドは、引数の型がレシーバの型と同一の場合は型パラメータを省くことができます。たとえば:

```swift
// Good
struct Composite<T> {
    …
    func compose(other: Composite) -> Composite {
        return Composite(self, other)
    }
}

// Bad
struct Composite<T> {
    …
    func compose(other: Composite<T>) -> Composite<T> {
        return Composite<T>(self, other)
    }
}
```

### 条件式
- **[MUST]** 条件式全体を囲う`()`は使わないこと

```swift
// Bad
if (a == 0) {
}

// Good
if a == 0 {
}
```

- **[SHOULD]** 条件式で値が確定する場合はなるべく let 宣言にすること
```swift
// Bad
var isOK = false
if a == 0 {  
    isOK = true
}

// Good
let isOK: Bool
if a == 0 {
    isOK = true
} else {
    isOK = false
}
```

- **[MUST]** Bool 判定の場合、冗長な書き方はしない
```swift
// Bad
if isOpen == true {
}

// Good
if isOpen {
}
```

- **[SHOULD]** Switch 文で `fallthrough` は使用しない

### クロージャー
- **[MUST]** 引数のクロージャーが 1 つだけの場合、Trailing Closure を利用すること

```swift
// Good
client.search(for: "Sushi") { recipes in
}
```

- **[MUST]** 引数がクロージャー 1 つだけの場合、`()`を省略すること

```swift
// Good
let titles = recipes.map { $0.title }
```

- **[MUST]** クロージャーの定義が 1 行だけの場合は shorthand argument を利用すること。逆に複数行にわたる場合は利用を避けること

```swift
// Good
let titles = recipes.map { $0.title }
```

```swift
// Good
client.search(for: "Sushi") { results, error in
    if error != nil {
        recipes = results
    }
}
```

- **[MUST]** 引数としてブロックを受け取るとき、`@escaping`は必要な場合のみ使用すること
- **[MUST]** `unowned`による変数キャプチャは避け、`weak`を使うこと
  - 適切に使用した場合はパフォーマンス改善に繋がるが、判断が難しくリスクを伴うため
  
### 例外
- **[MUST]** `NSException`を使用しないこと
- **[SHOULD]** `do` ~ `catch`を用いて、`try!`の使用は避けること

### オプショナル型の開示指定は避ける
- **[SHOULD]** `FooType?`もしくは`FooType!`型の変数`foo`がある場合、そこにある`foo!`を得ようとして`foo`に対して開示指定を行うのは可能な限り避けないといけません。
     * ただし、`@IBOutlet` など 値が確実にあることが保証されている場合はこの限りではない
```swift
// Good
if let foo = foo {
    // 開示された`foo`の値を使う
} else {
    // 必要であれば、ここでオプショナルがnilの場合の処理を行う
}
```

---
### 参考サイト
* https://github.com/jarinosuke/swift-style-guide
* https://docs.swift.org/swift-book/documentation/the-swift-programming-language
* https://www.swift.org/documentation/api-design-guidelines/
* https://github.com/linkedin/swift-style-guide
* https://google.github.io/swift/#source-file-basics
* https://github.com/airbnb/swift
* https://github.com/airbnb/swift?tab=readme-ov-file
* https://github.com/cookpad/styleguide/blob/master/swift.ja.md
