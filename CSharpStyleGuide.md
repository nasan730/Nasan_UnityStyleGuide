# C# StyleGuide<br>
## ぴよ
### ふが
#### ほげ

## ファイル名について
**パスカルケース**で、Unicode(UTF-8 シグネチャ付き)で作成してください。
```C#
ExampleComponent.cs
```
<br>

## usingディレクティブについて
ファイルの一番上に記述してください。<br>
基本的に`.`の数が少ない順かつアルファベット順で、以下の順序で記述してください。
1. [System名前空間](https://learn.microsoft.com/ja-jp/dotnet/api/system?view=net-7.0)
2.  [UnityEngine名前空間](https://docs.unity3d.com/ja/2023.2/ScriptReference/index.html)
3.  [Unity Registry](https://docs.unity3d.com/ja/2023.2/Manual/upm-ui-install.html)からインストールするパッケージ<br>
4.  GitHubなど外部から取得したソースコード名前空間
5.  NasanUtilityクラス
6.  プロジェクトの名前空間

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
// using 外部から取得したソースコードの名前空間;
using NasanUtility;
using Project.System;
```

## コメントについて
### 変数・関数に付けるコメント
 [XML Document](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/xmldoc/recommended-tags#summary)を使用して記述してください。<br>

Visual Studio 及び Rider等を使用しているのであれば`/`を三回押すことで<br>
自動的に`<summary>`が付きます。

```C#
/// <summary> 数 </summary>
private int _number = 0;

/// <summary>
/// 引数にインクリメントを行う関数
/// </summary>
/// <param name="num">数</param>
/// <returns>数</returns>
private int NumberIncriment(int num)
{
    return num++;
}
```
一般的に推奨されるXMLタグは以下の通りです。

| XMLタグ | 内容 |
| --- | --- |
| `<summary> XXX </summary>` | 変数・関数に補足情報を付ける |
| `<param name="name"> XXX </param>` | `name`: 関数の引数名が入る<br>引数に補足情報を付ける |
| `<returns> XXX </returns>` | 関数の戻り値に補足情報を付ける |
| `<inheritdoc/>` | virtual関数をoverrideしている関数に付ける<br>基底クラスのXMLで記述した内容がそのまま使用される |
<br>

### セパレータコメント
コードの可読性を上げるため、使用してください。<br>
区切り線は`-`を使用し、70文字です。<br>
コメント`//`と`-`の間には半角スペース一文字開けてください。<br>
コメント文は**一行で簡潔**に記述してください。<br>
```C#
// ----------------------------------------------------------------------
// セパレータコメント
// ----------------------------------------------------------------------
```
<br>

### コメント
コードだけでは意図が伝わらない場合、**簡潔で分かりやすいコメントを心がけてください。**<br>

目安としては**一行半角50文字、全角25文字以内とし、最大で3行まで**に収めてください。<br>
それが難しい場合は、処理内容を一度分割して簡潔に説明出来るように考え直してください。[^1]<br>

コメントは`//`を使用し、半角スペースを空けて記述してください。<br>
`/* */`は使用禁止です。<br>
```C#
// コメントの一例
// コメントは短く簡潔に
// 全角２５文字はこれくらい！！！！！！！！！！！！！
```

TODOコメントやFIXMEコメント等は推奨しています。<br>
文字数制限は上記の通り、行数に制限はありません。<br>
ただし、修正したら速やかに消してください。<br>

`TODO`や`FIXME`の後にはコロンと半角スペースを開けて自身のハンドルネームを記述し、<br>
その後にコメントを記述してください。
```C#
// TODO: H.N.
//       そのうち修正を行う

// FIXME: H.N.
//       もっとより良い処理を行うべき
//       具体的には…
//       ほげふが…
```
<br>

## Tab・スペースについて
Tabは一般的な半角スペース4つ分のものを使用してください。<br>

半角スペースについては下記の表を参考にしてください。
| 半角スペースを | 対象 |
| --- | --- |
| 空ける | `if for foreach while`<br>カンマ`,`<br>算術演算子`+ - * / % =`<br>比較演算子`> < & |` |
| 空けない | 論理否定演算子`!`<br>インクリメント`++`<br>デクリメント`--`|


```C#
/// <summary>
/// スペースのサンプル
/// </summary>
/// <param name="num">数</param>
/// <param name="flg">フラグ</param>
private void ExampleSpaceFunction(int num, bool flg)
{
    // 算術・比較演算子は付ける
    int total = num + num;
    if (total >= 0)
    {
        // インクリメントには付けない
        total++;
    }
    
    // 論理否定演算子は付けない
    if (!flg)
    {
        flg = !flg;
    }
}
```

## 中括弧について
字下げオールマンスタイルを使用してください。<br>
nullチェックやフラグチェックの場合は、かつ一行で完結出来るものであれば中括弧なしで早期リターンを行ってください。<br>
後述しますが、ラムダ式・Getter/Setterに関しては1行で記述できるのであれば1行で記述してください<br>

```C#
/// <summary>
/// 中括弧のサンプル
/// </summary>
/// <param name="num">数</param>
private void ExampleScope(int num)
{
    // 早期リターンは一行でOk
    if (num > 0) return;
    if (!_flg) return;

    if (true)
    {
        // 処理
    }
    else
    {
        // 処理
    }
}
```

## クラス内順序について
### 修飾子順序について
以下の順序で記述してください。<br>
1. `public`
2. `protected`
3. `internal`
4. `private`
5. `new`
6. `abstract`
7. `override`
8. `readonly`
9. `extern`
10. `unsafe`
11. `volatile`
12. `async`
<br>

### メンバー・要素順序について
以下の順序で記述してください。
1. `static const readonly` フィールド
2. `public protected private` フィールド
3. `get set`プロパティ
4. `Action Func`等のデリゲート
5. コンストラクタ・デストラクタ
6. 継承関数
7. Unityメゾット
8. 公開関数
9. 内部関数
10. `enum struct class`



## 名前空間について
基本的にはAssets以下のフォルダ階層と同じで、**パスカルケース**で付けてください。<br>
ただし`Scripts`は省略します。<br>

例：`Assets/Project/Scripts/InGame/Player/PlayerMovement.cs`の場合<br>
```C#
namespace Project.InGame.Player
{
    /// <summary> プレイヤー移動 </summary>
    public class PlayerMovement
    {
        /// <summary> 移動速度 </summary>
        private float _speed = 1.0f;
    }
}
```
<br>

## クラス・構造体・インターフェースについて
クラス・構造体名は**パスカルケース**で記述してください。<br>
インターフェースクラスは頭に`I`を付けて**パスカルケース**で記述してください。
```C#
/// <summary> サンプルクラス </summary>
public class ExampleClass
{

}

/// <summary> サンプル構造体 </summary>
public struct ExampleStruct
{

}

/// <summary> サンプルインターフェース </summary>
public interface IExampleInterface
{

}
```

## 変数について
**キャメルケース**で記述してください。<br>
`private`な変数は頭に`_`を付けて**キャメルケース**で記述してください。<br>

```C#
public string name = "SuperName";
protected int maxHp = 10;
protected int _hp = 0;
```

なお、inspectorに表示させる為だけに`public`修飾子を付けるのは控えてください。<br>
初期値を変更するのであれば`[Serializefield]`属性を付けた`private`変数を検討してください。<br>

データ用のクラス(例えばプレイヤーのパラメータなど)のクラスであれば、<br>
`public`変数を使用しても構いません。<br>

変数名にクラスの役割を入れる場合は、末端にその名前を記述してください。<br>
```C#
using System;
using UnityEngine;

/// <summary> プレイヤークラス </summary>
public class Player : MonoBehaviour
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> パラメータ </summary>
    [Serializefield]
    private Parameter _playerParam = null;

    // ----------------------------------------------------------------------
    // Unityメゾット
    // ----------------------------------------------------------------------

    /// <summary>
    /// 初期化処理
    /// </summary>
    private void Start()
    {
        _param = new();
    }
}

/// <summary> パラメータクラス </summary>
[Serializable]
public class Parameter
{
    /// <summary> 体力 </summary>
    public int hp = 0;

    /// <summary> 攻撃力 </summary>
    public int attack = 0;
}
```


## field初期化について
変数の宣言と同時に初期化をしてください。
```C#
private int _num = 0;

private RigidBody _rigidBody = null;
```

## getter・setterについて
### getterプロパティについて
`{ get XXX; }` ・ `=>`どちらを使用しても構いませんが、こだわりがなければ`=>`を使用してください。<br>
また、1行で記述してください。
```C#
private int _num = 0;

// 推奨getter
public int num => _num;

// こちらでもOK
public int number { get _num; }
```

値を変換・計算して値を渡す場合は、<br>
`getter`プロパティを使用せず、頭に`Get`を付けた関数で渡すようにしてください。

```C#
private int _num = 0;

// NG
//public int num => _num + 1;

// OK
/// <summary>
/// 計算した数を取得
/// </summary>
/// <returns>計算した数</returns>
public int GetNumber()
{
    return _num + 1;
}
```

### setterプロパティについて
**使用しないでください。**<br>
`private`変数に`setter`を付けることは、`public`変数で自由に値を変更していることと同じです。<br>

値を変更したい場合は、どこから参照されているかがデバッグしやすくするため、<br>
頭に`Set`を付けた関数で値を設定して下さい。<br>
```C#
private int _num = 0;

// NG
//public int num { set value; }

// OK
/// <summary>
/// 値を設定
/// </summary>
/// <param name="num">数</param>
public int SetNumber(int num)
{
    if (num > 0) return;
    
    _num = num;
}
```

## 定数について
**パスカルケース**で、記述してください。
```C#
public static int StaticNumber = 0;
public const int ConstantNumber = 0;
```

## 列挙型について
**パスカルケース**で、記述してください。<br>
一番最初の列挙名には初期値`=0`を付け、<br>
除外用の列挙名にはその列挙型内の最低値を入れてください。<br>
```C#
/// <summary> 状態異常 </summary>
public enum Condition
{
    Normal      = 0,  // 通常
    Poison,           // 毒
    Paralysis,        // マヒ
    Sleep,            // 眠り
    Dead,             // 死亡
    Max,              // 最大
    None        = -1; // 除外
}
```

フラグ用の列挙型には`[Flags]`属性を付け、<br>
シフト演算子で記述してください。<br>
```C#
/// <summary> 状態異常 </summary>
[Flags]
public enum Condition
{
    Normal      = 0,    // 通常
    Poison      = 1<<1, // 毒
    Paralysis   = 1<<2, // マヒ
    Sleep       = 1<<3, // 眠り
    Dead        = 1<<4, // 死亡
    Max         = 1<<5, // 最大
}
```


## 属性について
`Serializefield`を使用しているのであれば一番上に記述し、<br>
それ以降はアルファベット順で、属性1つごとに改行して記述してください。<br>
```C#
[Serializefield]
[Min(0)]
[Max(10)]
private int _num = 0;
```

## デリゲートについて
基本的に`private`で作成し、末尾に`CallBacks`を付けて**キャメルケース**で記述してください。<br>
デリゲートに関数を登録・解除する場合は[デリゲート関連の関数ルール](#デリゲート関連の関数ルール)を参考に作成してください。

## ラムダ式について
一行で記述出来るのであれば一行で記述してください。
二行以上になる場合は**括弧を付けて字下げオールマンスタイル**を使用してください。<br>
```C#
Action<int, int> action = null;

// 一行で収まる場合
action = x => x + 1 ;

// 二行以上になる場合
action = (x) => 
         {
            int ret = 0;
            ret = x * x;
            return ret;
         };
```

## 関数について
### 共通ルール
**パスカルケース**で、記述してください。<br>
**行数が50行を超えそうな場合、処理を切り分けることが出来ないか検討してください。**<br>
```C#
/// <summary> サンプル関数 </summary>
private void ExampleFunction()
{
    // 処理
}
```

### 初期化・終了処理を行う関数のルール
初期化を行う場合は頭に`Initialize`、
終了処理を行う場合は頭に`Finalize`を付けてください。

初期化・終了処理の後に続く関数名が存在する場合に限り、
`InitXXX`・`FinalXXX`と記述しても構いません。

```C#
/// <summary> 初期化 </summary>
public void Initialize()
{
    InitStatus();
}

/// <summary> 終了処理 </summary>
public void Finalize()
{
    FinalStatus();
}

/// <summary> ステータスの初期化 </summary>
private void InitStatus()
{
    // 処理
}

/// <summary> ステータスの終了処理 </summary>
private void FinalStatus()
{
    // 処理
}
```

### デリゲート関連の関数ルール
デリゲートに関数を**渡す側**は頭に`On`を付けて記述してください。
```C#
using UnityEngine;

/// <summary> デリゲートサンプルクラス </summary>
public class ExampleClass : MonoBehaviour
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> デリゲートクラス </summary>
    private ExampleDelegate _example = null;

    // ----------------------------------------------------------------------
    // Unityメゾット
    // ----------------------------------------------------------------------

    /// <summary>
    /// 初期化処理
    /// </summary>
    private void Start()
    {
        _example = new();
        _example.AddSampleCallBack(OnShowLog);
    }

    // ----------------------------------------------------------------------
    // 内部関数
    // ----------------------------------------------------------------------

    /// <summary>
    /// ログの表示
    /// </summary>
    private void OnShowLog()
    {
        Debug.Log("Hello!");
    }
}

```


デリゲートに関数を**登録・解除される**側は以下のルールを参考に作成してください。

| 条件 | 関数名 |
| --- | --- |
| 関数を**登録**する | `RegisterXXXCallBack` |
| 関数を**解除**する | `UnregisterXXXCallBack`|
| 関数を**全解除**する | `AllUnregisterXXXCallBack`|
| 関数を**追加**する | `AddXXXCallBack`|
| 関数を**除外**する | `RemoveXXXCallBack`|
| 関数を**全除外**する | `AllRemoveXXXCallBack`|

<details>

<summary>サンプルコード</summary>

```C#
/// <summary> デリゲートサンプルクラス </summary>
public class ExampleDelegate
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> デリゲートサンプル </summary>
    private Action _sampleCallBacks = null;

    /// <summary>
    /// デリゲートの登録
    /// </summary>
    /// <param name="callBack">デリゲート</param>
    public void RegisterSampleCallBack(Action callBack)
    {
        _sampleCallBacks = callBack;
    }

    /// <summary>
    /// デリゲートの解除
    /// </summary>
    /// <param name="callBack">デリゲート</param>
    public void UnregisterSampleCallBack(Action callBack)
    {
        if(callBack == _sampleCallBacks)
        {
            _sampleCallBacks = null;
        }
    }

    /// <summary>
    /// デリゲートの全解除
    /// </summary>
    public void AllUnregisterSampleCallBack()
    {
        _sampleCallBacks = null;
    }

    /// <summary>
    /// デリゲートの追加
    /// </summary>
    /// <param name="callBack">デリゲート</param>
    public void AddSampleCallBack(Action callBack)
    {
        _sampleCallBacks += callBack;
    }

    /// <summary>
    /// デリゲートの除外
    /// </summary>
    /// <param name="callBack">デリゲート</param>
    public void RemoveSampleCallBack(Action callBack)
    {
        _sampleCallBacks -= callBack;
    }

    /// <summary>
    /// デリゲートの全除外
    /// </summary>
    /// <param name="callBack">デリゲート</param>
    public void AllRemoveSampleCallBack()
    {
        _sampleCallBacks = callBack;
    }
}
```

</details>


### コルーチンの関数ルール
頭に`Coroutine`を付けて記述してください。
```C#
/// <summary> サンプルコルーチン </summary>
private IEnumerator CoroutineExample() 
{
    // 処理
}
```


## verについて
[組み込み型](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/built-in-types)についてはvarを使用しないでください。<br>
それ以外の型については**型が明示されているのであれば**使用しても構いません。<br>
```C#
// NG
int num = 0;
//var tmp = num;

// OK
var rb = GetComponent<Rigidbody>();
```

## ref・outについて

## ログ・アサーションについて

## コピーライトについて

### サンプルコード
長いので折りたたみ。

<details>

<summary>サンプルコード</summary>

```C#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

namespace Project.Example
{
    /// <summary> サンプルインターフェース </summary>
    public abstract class IExampleInterface
    {
        // ----------------------------------------------------------------------
        // 継承関数
        // ----------------------------------------------------------------------

        /// <summary>
        /// 継承関数
        /// </summary>
        protected abstract void InheritanceFunction();
    }

    /// <summary> サンプルクラス </summary>
    public class ExampleClass : MonoBehaviour, IExampleInterface
    {
        // ----------------------------------------------------------------------
        // 定数
        // ----------------------------------------------------------------------

        /// <summary> 静的ナンバー </summary>
        public static int StaticNumber = 1;

        /// <summary> 定数ナンバー </summary>
        public const int ConstantNumber = 1;

        // ----------------------------------------------------------------------
        // 変数
        // ----------------------------------------------------------------------

        /// <summary> ステータス </summary>
        private Status _status;

        /// <summary> 公開ナンバー </summary>
        public int freeNumber = 1;

        /// <summary> 継承ナンバー </summary>
        protected int inheritanceNumber = 1;
        
        /// <summary> 内部ナンバー </summary>
        private int _number = 1;

        /// <summary> ナンバーのゲッター </summary>
        public int nummber => _number;

        /// <summary> デリゲート </summary>
        public Action _exampleCallBacks = null;

        // ----------------------------------------------------------------------
        // コンストラクタ
        // ----------------------------------------------------------------------

        /// <summary>
        /// コンストラクタ
        /// </summary>
        public ExampleClass()
        {
            
        }
        
        // ----------------------------------------------------------------------
        // 継承関数
        // ----------------------------------------------------------------------

        /// <inheritdoc/>
        protected override InheritanceFunction()
        {
            Debug.Log("継承！");
        }

        // ----------------------------------------------------------------------
        // Unityメゾット
        // ----------------------------------------------------------------------

        /// <summary>
        /// 初期化処理
        /// </summary>
        private void Start()
        {
            Initalize();
        }

        /// <summary>
        /// 破壊時処理
        /// </summary>
        private void OnDestroy()
        {
            AllUnRegisterCallBacks();
        }

        // ----------------------------------------------------------------------
        // 公開関数
        // ----------------------------------------------------------------------

        /// <summary>
        /// 初期化
        /// </summary>
        public Initalize()
        {
            PrintDebugLog("初期化！");
        }

        /// <summary>
        /// デリゲート登録
        /// </summary>
        public RegisterCallBack(Action callBack)
        {
            _exampleCallBacks += callBack;
        }

        /// <summary>
        /// デリゲート解除
        /// </summary>
        public UnRegisterCallBack(Action callBack)
        {
            _exampleCallBacks -= callBack;
        }

        /// <summary>
        /// デリゲートを全解除
        /// </summary>
        public AllUnRegisterCallBacks()
        {
            _exampleCallBacks = null;
        }

        // ----------------------------------------------------------------------
        // 内部関数
        // ----------------------------------------------------------------------

        /// <summary>
        /// デバッグログ表示
        /// </summary>
        /// <param name="text">テキスト</param>
        private void PrintDebugLog(string text)
        {
            Debug.Log(text);
        }
        
        // ----------------------------------------------------------------------
        // クラス
        // ----------------------------------------------------------------------

        /// <summary> ステータス </summary>
        private class Status
        {
            /// <summary> 体力 </summary>
            public hp = 0;
            
            /// <summary> 魔力 </summary>
            public mp = 0;
        }

    }
}

```

</details>

<br>

[^1]:あくまでたとえであり実際にそうしろとは言いませんが、極力長いコメントは避けるべきです。