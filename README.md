objective-c
===========

コンパイラディレクティブ
---
コンパイラに対する Objective-C のディレクティブはすべて「@」で始まる
- @interface ~ @end
 - クラスの宣言（.hファイルで。）
- @implementation ～ @end
 - クラスの実装（.mファイルで。）

クラスの宣言
---
@interface クラス名：スーパークラス名 <プロトコル>

こんなの`@interface HelloWorld : NSObject <UIApplicationDelegate>`
- プロトコル
 - メソッドの宣言（プロトタイプ宣言）の集合
 - Objective-Cでは単一継承というルールがある
 - どうしても呼びたくなったら、＜カッコ＞付けてプロトコルとして呼ぶ
 - カンマで区切れば何個でも呼ぶことができる
 - プロトコルはメソッドの宣言だけで実装部分がないという制限つき

インスタンス変数
---
こんなの
```
IBOutlet UIWindow *window;
MyViewController *myViewController;
```
- `IBOutlet` アウトレットとして使う
- `UIWindow` クラスオブジェクト型
- `*window` 変数名
 - 型がクラスオブジェクト型の場合は、変数名の頭にアスタリスクを付ける 

メソッド
---
こんなの
`- (void) applicationDidFinishLaunching:(UIApplication *)application {}`
- `-`
 - インスタンスメソッド
     - インスタンスになったときだけ有効なメソッド 
 - クラスメソッドの場合は`+`
     - インスタンスにしなくてもクラスで使えるメソッド
- `(void)` 
 - 戻り値の型
- `applicationDidFinishLaunching`
 - 変数名
- `(UIApplication *)`
 - 引数の型
 - クラスオブジェクト型のときは`*`をつける
- `application`
 - 引数名

メソッドの呼び出し
---
こんなの
```
[MyViewController alloc]
[window addSubview:controllersView]
[[MyViewController alloc] initWithNibName:@"HelloWorld" bundle:[NSBundle mainBundle]];
```
- [[オブジェクト名 メソッド名1:引数1] メソッド名2:引数2 引数3]
 - （オブジェクト名）が（引数1）を受け取って（メソッド名1）をした結果を、（引数2）と（引数3）を引数として（メソッド名2）する 

アクセサメソッドの自動生成
---
`@property`と`@synthesize`。
アクセサメソッドの自動生成用コンパイラディレクティブ
ゲッターとセッターを作ってくれる。
こんなん
```
@property (nonatomic, retain) UIWindow *window;
@property (nonatomic, retain) MyViewController *myViewController;
@synthesize window;
@synthesize myViewController;
```
- @property（オプション）インスタンス変数型 インスタンス変数名;
 - 宣言部分に書く
 - オプション
     - nonatomic
         - 複数のスレッドが同時に実行されている場合に動作を保証しない
     - atomic
         - 複数のスレッドが同時に実行されているか否かに関係なくインスタンス変数の値を完全に取得/設定する（デフォルト）
     - assign
         - プロパティで受け取った値をインスタンス変数に単純に代入する
         - int型などのパラメトリックな変数はassignしか指定できないため、指定を省略可能
     - retain
         - プロパティで受け取った値をインスタンス変数に代入し、メモリ上に確保されたインスタンスの領域が勝手にメモリ上から破棄されないようにする
     - copy
         - プロパティで受け取った値をコピーして、その領域へのポインタをインスタンス変数に代入し、コピーされた領域が勝手にメモリ上から破棄されないようにする
     - readonly
         - 読み取り専用 
     - readwrite
         - 読み書き可能（デフォルト） 
- @synthesize インスタンス変数名
 - 実装部分に書く
