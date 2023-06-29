# C# StyleGuide<br>

## ファイル名について
**パスカルケース**で、Unicode(UTF-8 シグネチャ付き)で作成してください。
```C#
ExampleComponent.cs
```
<br>

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

### サンプルコード
折りたたみ

```C#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

namespace Project.Example
{
    /// <summary> 数クラス </summary>
    public abstract class ExampleNumber : MonoBehaviour
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

        /// <summary> 公開ナンバー </summary>
        public int freeNumber = 1;

        /// <summary> 継承ナンバー </summary>
        protected int inheritanceNumber = 1;
        
        /// <summary> 内部ナンバー </summary>
        private int _number = 1;

        // ----------------------------------------------------------------------
        // 継承関数
        // ----------------------------------------------------------------------

        /// <summary>
        /// 継承関数
        /// </summary>
        protected abstract void InheritanceFunction();
    }

    /// <summary> サンプルクラス </summary>
    public class ExampleClass : ExampleNumber
    {
        // ----------------------------------------------------------------------
        // 変数
        // ----------------------------------------------------------------------

        /// <summary> ステータス </summary>
        private Status _status;

        /// <summary> ナンバーのゲッター </summary>
        public int GetNummber => freeNumber;

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

<br>

## 変数について
**キャメルケース**で記述してください。<br>
`private`な変数は頭に`_`を付けて**キャメルケース**で記述してください。

```C#
public string name = "SuperName";
protected int maxHp = 10;
protected int _hp = 0;
```

## 列挙型・定数について

## getter・setterについて

## 属性について

## ref・out・verについて

## field初期化について

## ログ・アサーションについて

## コピーライトについて

[^1]:あくまでたとえであり実際にそうしろとは言いませんが、極力長いコメントは避けるべきです。