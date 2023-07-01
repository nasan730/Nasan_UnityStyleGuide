# C# StyleGuide<!-- omit in toc -->

## 目次

- [1. ファイル名について](#1-ファイル名について)
- [2. コピーライト表記について](#2-コピーライト表記について)
- [3. usingディレクティブについて](#3-usingディレクティブについて)
- [4. コメントについて](#4-コメントについて)
  - [4.1. 変数・関数に付けるコメント](#41-変数関数に付けるコメント)
  - [4.2. セパレータコメント](#42-セパレータコメント)
- [5. Tab・スペースについて](#5-tabスペースについて)
- [6. 中括弧について](#6-中括弧について)
- [7. クラス内順序について](#7-クラス内順序について)
  - [7.1. 修飾子](#71-修飾子)
  - [7.2. 変数・関数](#72-変数関数)
- [8. 名前空間について](#8-名前空間について)
- [9. クラス・構造体・インターフェースについて](#9-クラス構造体インターフェースについて)
- [10. 変数について](#10-変数について)
- [11. field初期化について](#11-field初期化について)
- [12. getter・setterについて](#12-gettersetterについて)
  - [12.1. getterプロパティ](#121-getterプロパティ)
  - [12.2. setterプロパティ](#122-setterプロパティ)
- [13. 定数について](#13-定数について)
- [14. 列挙型について](#14-列挙型について)
- [15. 属性について](#15-属性について)
- [16. デリゲートについて](#16-デリゲートについて)
- [17. ラムダ式について](#17-ラムダ式について)
- [18. 関数について](#18-関数について)
  - [18.1. 初期化・終了処理を行う関数のルール](#181-初期化終了処理を行う関数のルール)
  - [18.2. デリゲート関連の関数ルール](#182-デリゲート関連の関数ルール)
  - [18.3. コルーチンの関数ルール](#183-コルーチンの関数ルール)
- [19. 引数について](#19-引数について)
  - [19.1. デフォルト引数・ref・out](#191-デフォルト引数refout)
- [20. verについて](#20-verについて)
- [21. タプルについて](#21-タプルについて)
- [22. ログ・アサーションについて](#22-ログアサーションについて)
- [23. サンプルコード](#23-サンプルコード)

<br>
<br>
<br>

# 1. ファイル名について
**パスカルケース**で、Unicode(UTF-8 シグネチャ付き)で作成してください。<br>
基本的に**一つのファイルに一つのクラス**を作成して下さい。<br>
定義用のクラス等は複数作成しても構いません。<br>

```C#
ExampleComponent.cs
```
<br>
<br>
<br>

# 2. コピーライト表記について
ソースコードの一番上に以下のコメント文を追加してください。<br>
下記の表を見て単語を置き換えてください。
| 単語 | 変更内容 |
| --- | --- |
| `XXX.cs` | ソースコードのファイル名 |
| `説明` | ソースコードの簡易な説明 |
| `YEAR` | 現在の西暦 |
| `YOUR_NAME` | 作成者名 |

```C#
/**
 *  FileName    :   XXX.cs
 *  Description :   説明
 *
 *  Copyright YEAR YOUR_NAME All rights reserved.
 */
```
<br>
<br>
<br>

# 3. usingディレクティブについて
ソースコードの[コピーライト表記](#2-コピーライト表記について)の次に記述してください。<br>
基本的に`.`の**数が少ない順**かつ**アルファベット順**で、以下の順序で記述してください。
1. [System名前空間](https://learn.microsoft.com/ja-jp/dotnet/api/system?view=net-7.0)
2.  [UnityEngine名前空間](https://docs.unity3d.com/ja/2023.2/ScriptReference/index.html)
3.  [Unity Registry](https://docs.unity3d.com/ja/2023.2/Manual/upm-ui-install.html)からインストールしたパッケージのソースコードの名前空間<br>
4.  GitHubなど外部から取得したソースコードの名前空間
5.  NasanUtility名前空間
6.  プロジェクトのゲーム系統の名前空間
7.  プロジェクトのシステム系統の名前空間

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
// using 外部から取得したソースコードの名前空間;
using NasanUtility;
using Project.InGame.Example;
using Project.System;
```
<br>
<br>
<br>

# 4. コメントについて
コードだけでは意図が伝わらない場合、**簡潔で分かりやすいコメントを心がけてください。**<br>

目安としては**一行半角50文字、全角25文字以内とし、最大で3行まで**に収めてください。<br>
それが難しい場合は、処理内容を一度分割して簡潔に説明出来るように考え直してください。<br>

コメントは`//`を使用し、半角スペースを空けて記述してください。<br>
`/* */`は使用禁止です。<br>
```C#
// コメントの一例
// コメントは短く簡潔に
// 全角２５文字はこれくらい！！！！！！！！！！！！！
```
<br>

TODOコメントやFIXMEコメント等は使用して構いません。<br>
文字数制限は同じく**一行半角50文字、全角25文字以内**、行数に制限はありません。<br>
必要無くなった場合、速やかに消してください。<br>

`TODO`や`FIXME`の後にはコロン`:`と半角スペースを開けて**コメント作成者の名前を記述**し、<br>
その後コメントを記述してください。
```C#
// TODO: YOUR_NAME
//       そのうち修正を行う

// FIXME: YOUR_NAME
//        もっとより良い処理を行うべき
//        具体的には…
//        さらに…
```
<br>
<br>
<br>

## 4.1. 変数・関数に付けるコメント
 [XML Document](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/xmldoc/recommended-tags#summary)を使用して**記述してください**。<br>

一般的に推奨されるXMLタグは以下の通りです。

| XMLタグ | 内容 |
| --- | --- |
| `<summary> XXX </summary>` | 変数・関数に補足情報を付ける |
| `<param name="name"> XXX </param>` | `name`: 関数の引数名が入る<br>引数に補足情報を付ける |
| `<returns> XXX </returns>` | 関数の戻り値に補足情報を付ける |
| `<inheritdoc/>` | virtual関数をoverrideしている関数に付ける<br>基底クラスのXMLで記述した内容がそのまま使用される |
<br>

```C#
/// <summary> 変数 コメントサンプル </summary>
private int _num = 0;

/// <summary>
/// 関数 コメントサンプル
/// インクリメントを行う関数
/// </summary>
/// <param name="num">数</param>
/// <returns>数</returns>
private int ExampleFunction(int num)
{
    return num++;
}
```
<br>
<br>
<br>

## 4.2. セパレータコメント
ソースコードの可読性を上げるため、**記述してください**。<br>
区切り線は`-`を使用し、70文字です。<br>
コメント`//`と`-`の間には半角スペース一文字開けてください。<br>
コメント文は**一行で簡潔**に記述してください。<br>
```C#
// ----------------------------------------------------------------------
// セパレータコメント
// ----------------------------------------------------------------------
```
<br>
<br>
<br>

# 5. Tab・スペースについて
Tabは**半角スペース4つ分**のものを使用してください。<br>

半角スペースについては下記の表を参考にしてください。
| 半角スペースを | 対象 |
| --- | --- |
| 空ける | `if for foreach while`<br>カンマ`,`<br>算術演算子`+ - * / % =`<br>比較演算子`> < & \|` |
| 空けない | 論理否定演算子`!`<br>インクリメント`++`<br>デクリメント`--`|
<br>

```C#
/// <summary>
/// スペースのサンプル
/// </summary>
/// <param name="num">数</param>
/// <param name="flg">フラグ</param>
private void ExampleFunction(int num, bool flg)
{
    // 算術・比較演算子は空ける
    // ifと()の間を空ける
    int total = num + num;
    if (total >= 0)
    {
        // インクリメントには空けない
        total++;
    }
    
    // 論理否定演算子は空けない
    if (!flg)
    {
        flg = !flg;
    }
}
```
<br>
<br>
<br>

# 6. 中括弧について
**字下げオールマンスタイル**を使用してください。<br>

`null`チェックやフラグのチェックなど、早期リターンを行う`if`文の場合は、<br>
**一行で完結出来るものに限り**中括弧なしで早期リターンを行ってください。<br>

[Getter/Setter](#12-getter・setterについて)・[ラムダ式](#17-ラムダ式について)に関しては**一行で完結出来るものに限り**一行で記述してください。<br>

```C#
/// <summary>
/// 中括弧のサンプル
/// </summary>
private void ExampleFunction()
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
<br>
<br>
<br>

# 7. クラス内順序について
## 7.1. 修飾子
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
<br>
<br>

## 7.2. 変数・関数
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
<br>
<br>
<br>

# 8. 名前空間について
基本的にはAssets以下のフォルダ階層と同じで、**パスカルケース**で付けてください。<br>
ただし`Assets`と`Scripts`は省略します。<br>

例：`Assets/Project/Scripts/InGame/Example/ExampleClass.cs`の場合<br>
```C#
namespace Project.InGame.Example
{
    /// <summary> サンプルクラス </summary>
    public class ExampleClass
    {
        // クラス内の記述
    }
}
```
<br>
<br>
<br>

# 9. クラス・構造体・インターフェースについて
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
<br>
<br>
<br>

# 10. 変数について
**キャメルケース**で記述してください。<br>
`private`変数は頭に`_`を付けて**キャメルケース**で記述してください。<br>

```C#
public string publicName = "Name";
protected int protectedNum = 10;
private int _privateNum = 0;
```
<br>

**inspectorに設定させる目的**だけで`public`修飾子を付けるのは**控えてください**。<br>

inspector設定させたいのであれば[`Serializefield`](https://docs.unity3d.com/ja/2023.2/ScriptReference/SerializeField.html)属性を付けた`private`変数を追記したり、<br>
[`Serializable`](https://docs.unity3d.com/ja/2023.2/ScriptReference/Serializable.html)属性を付けたデータ用の`class`を作成し、<br>
作成したデータ用`class`を[`Serializefield`](https://docs.unity3d.com/ja/2023.2/ScriptReference/SerializeField.html)属性つけて`private`変数として扱うなどしてください。

<details>

<summary>サンプルコード</summary>

```C#
using System;
using UnityEngine;

/// <summary> サンプルクラス </summary>
public class ExampleClass : MonoBehaviour
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> パラメータクラス </summary>
    [Serializefield]
    private ExampleParameter _playerParam = null;

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
public class ExampleParameter
{
    /// <summary> 体力 </summary>
    public int hp = 0;

    /// <summary> 攻撃力 </summary>
    public int attack = 0;
}
```

</details>
<br>
<br>
<br>

# 11. field初期化について
**変数の宣言と同時に初期化**をしてください。
クラス・構造体の初期化を行う場合、`new()`を使用してください。
```C#
/// <summary> 変数サンプル </summary>
private int _num = 0;

/// <summary> 変数クラスサンプル </summary>
private ExampleClass _example = null;

/// <summary>
/// 初期化
/// </summary>
public void Initialize()
{
    _example = new();
}
```
<br>
<br>
<br>

# 12. getter・setterについて
## 12.1. getterプロパティ
`{ get XXX; }` ・ `=>`どちらを使用しても構いませんが、こだわりがなければ`=>`**を使用してください。**<br>
また、1行で記述してください。<br>
```C#
private int _num = 0;

// ◎ 推奨するgetter記述
public int num => _num;

// 〇 こちらでもOK
public int number { get _num; }
```
<br>

値を変換・計算して値を取得する場合は、<br>
`getter`プロパティを使用せず、頭に`Get`を付けた関数で取得するようにしてください。<br>

```C#
private int _num = 0;

// × NG
//public int num => _num + 1;

// 〇 OK
/// <summary>
/// 計算した数を取得
/// </summary>
/// <returns>計算した数</returns>
public int GetNumber()
{
    return _num + 1;
}
```
<br>
<br>
<br>

## 12.2. setterプロパティ
**使用しないでください。**<br>
`private`変数に`setter`を付けることは、`public`変数で自由に値を変更してしまっている事と同じです。<br>

値を変更したい場合、**どこから参照されているかをデバッグしやすくするため**に<br>
頭に`Set`を付けた**関数で値を設定させるようにしてください**。<br>
```C#
private int _num = 0;

// × NG
//public int num { set value; }

// 〇 OK
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
<br>
<br>
<br>

# 13. 定数について
**パスカルケース**で、記述してください。
```C#
public static int StaticNumber = 0;
public const int ConstantNumber = 0;
```
<br>
<br>
<br>

# 14. 列挙型について
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
<br>

フラグ用の列挙型には[`Flags`](https://learn.microsoft.com/ja-jp/dotnet/api/system.flagsattribute?view=net-7.0)属性を付け、<br>
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
<br>
<br>
<br>

# 15. 属性について
[`Serializefield`](https://docs.unity3d.com/ja/2023.2/ScriptReference/SerializeField.html)を**使用しているのであれば一番上に記述**し、<br>
それ以降は**属性一つごとに改行して記述**してください。<br>
```C#
[Serializefield]
[Min(0)]
[Max(10)]
private int _num = 0;
```
<br>
<br>
<br>

# 16. デリゲートについて
基本的に`private`で作成し、末尾に`CallBacks`を付けて**キャメルケース**で記述してください。<br>

デリゲートに関数を登録・解除する時は[デリゲート関連の関数ルール](#182-デリゲート関連の関数ルール)を参考に作成してください。
<br>
<br>
<br>

# 17. ラムダ式について
一行で記述出来るのであれば一行で記述してください。<br>
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
<br>
<br>
<br>

# 18. 関数について
**パスカルケース**で、記述してください。<br>
**行数が50行を超えそうな場合、処理を切り分けることが出来ないか検討してください。**<br>
```C#
/// <summary>
/// サンプル関数
/// </summary>
private void ExampleFunction()
{
    // 処理
}
```
<br>
<br>
<br>

## 18.1. 初期化・終了処理を行う関数のルール
初期化を行う場合は頭に`Initialize`、
終了処理を行う場合は頭に`Finalize`を付けてください。

要素ごとに切り分けて初期化・終了処理をさせる関数の場合、
`InitXXX`・`FinalXXX`と記述してください。

```C#
/// <summary>
/// 初期化 
/// </summary>
public void Initialize()
{
    InitStatus();
}

/// <summary>
///  終了処理
///  </summary>
public void Finalize()
{
    FinalStatus();
}

/// <summary>
///  ステータスの初期化
///  </summary>
private void InitStatus()
{
    // 処理
}

/// <summary> 
/// ステータスの終了処理 
/// </summary>
private void FinalStatus()
{
    // 処理
}
```
<br>
<br>
<br>

## 18.2. デリゲート関連の関数ルール
デリゲートに関数を**登録・解除される**側は以下のルールを参考に作成してください。

| 条件 | 関数名 |
| --- | --- |
| 関数を**追加**する | `AddXXXCallBack`|
| 関数を**除外**する | `RemoveXXXCallBack`|
| 関数を**全除外**する | `AllRemoveXXXCallBacks`|
| 関数を**登録**する | `RegisterXXXCallBack` |
| 関数を**解除**する | `UnregisterXXXCallBack`|
| 関数を**全解除**する | `AllUnregisterXXXCallBacks`|


<details>

<summary>サンプルコード</summary>

```C#
using System;

/// <summary> サンプル デリゲート管理クラス </summary>
public class ExampleDelegateManagement
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> デリゲートサンプル </summary>
    private Action _sampleCallBacks = null;

    // ----------------------------------------------------------------------
    // 公開関数
    // ----------------------------------------------------------------------

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
        _sampleCallBacks = null;
    }

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
    public void AllUnregisterSampleCallBacks()
    {
        _sampleCallBacks = null;
    }
}
```

</details>
<br>
<br>

デリゲートに関数を**渡す側**は頭に`On`を付けて記述してください。

<details>

<summary>サンプルコード</summary>

```C#
using UnityEngine;

/// <summary> サンプルクラス </summary>
public class ExampleClass : MonoBehaviour
{
    // ----------------------------------------------------------------------
    // 変数
    // ----------------------------------------------------------------------

    /// <summary> デリゲート管理 </summary>
    private ExampleDelegateManagement _example = null;

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

    /// <summary>
    /// 破壊時処理
    /// </summary>
    private void OnDestroy()
    {

        _example.RemoveSampleCallBack(OnShowLog);
        _example = null;
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

</details>
<br>
<br>
<br>

## 18.3. コルーチンの関数ルール
頭に`Coroutine`を付けて記述してください。
```C#
/// <summary> サンプルコルーチン </summary>
private IEnumerator CoroutineExample() 
{
    // 処理
}
```
<br>
<br>
<br>

# 19. 引数について
**キャメルケース**で記述してください。
```C#
/// <summary>
/// サンプル関数
/// </summary>
public void ExampleFunciton(string name, int num)
{
    // 処理
}
```
<br>
<br>
<br>

## 19.1. デフォルト引数・ref・out
[デフォルト引数](https://learn.microsoft.com/ja-jp/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments#optional-arguments) -> [`out`](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/out-parameter-modifier) -> [`ref`](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/ref) の順で記述してください。
```C#
public bool ExampleFunciton(int name, int num = 0, out int retNum)
{
    // 処理
    // return ...;
}
```
<br>
<br>
<br>

# 20. verについて
[組み込み型](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/built-in-types)についてはvarを使用しないでください。<br>
それ以外の型については**型が明示されているのであれば**使用しても構いません。<br>
```C#
// × NG
// int num = 0;
// var tmp = num;

// OK
var rb = GetComponent<Rigidbody>();
```
<br>
<br>
<br>

# 21. タプルについて
[タプル型](https://learn.microsoft.com/ja-jp/dotnet/csharp/language-reference/builtin-types/value-tuples)は、**そのクラスのスコープ内**であれば使用しても構いません。<br>
例えば、最小値と最大値を求めるときなどです。

タプルのフィールド名は**必ず記述**してください。
```C#
/// <summary>
/// サンプル関数
/// </summary>
private void ExampleFunciton()
{
    var minMax = GetMinMax();
}

/// <summary>
/// 最小と最大を記述
/// </summary>
private (int min, int max) GetMinMax()
{
    min = 0;
    max = 100;
}
```
<br>
<br>
<br>

# 22. ログ・アサーションについて
`System.Diagnostics`の[`Debug.Assert`](https://learn.microsoft.com/ja-jp/dotnet/api/system.diagnostics.debug.assert?view=net-7.0)ではなく、<br>
`UnityEngine.Assertions`の[`Assert`](https://docs.unity3d.com/ja/2021.1/ScriptReference/Assertions.Assert.html)を使用してください。<br>
<br>
<br>
<br>

# 23. サンプルコード
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
        public static int StaticNum = 1;

        /// <summary> 定数ナンバー </summary>
        public const int ConstantNum = 1;

        // ----------------------------------------------------------------------
        // 変数
        // ----------------------------------------------------------------------

        /// <summary> ステータスクラス </summary>
        private Status _status;

        /// <summary> 公開ナンバー </summary>
        public int publicNum = 1;

        /// <summary> 継承ナンバー </summary>
        protected int protectedNum = 1;
        
        /// <summary> 内部ナンバー </summary>
        private int _privateNum = 1;

        /// <summary> ナンバー </summary>
        public int nummber => _privateNum;

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
            _exampleCallBacks = null;
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
        public AddCallBack(Action callBack)
        {
            _exampleCallBacks += callBack;
        }

        /// <summary>
        /// デリゲート解除
        /// </summary>
        public RemoveCallBack(Action callBack)
        {
            _exampleCallBacks -= callBack;
        }

        /// <summary>
        /// デリゲートを全解除
        /// </summary>
        public AllRemoveCallBacks()
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

        /// <summary> ステータスクラス </summary>
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
<br>
<br>
