---
title: "ファイル一覧を取得する"
permalink: /filelist/
last_modified_at: 2021-11-07T00:00:00-02:00
toc: true
---

深さを指定してファイルとフォルダの一覧を取得し、テキストファイル`out.txt`へ出力する。

1行目、自作関数`GetList`の第1引数`"."`は、現在の作業フォルダを起点として探索する。

`"C:¥test"`などフォルダを直接指定しても良い。

第2引数は探索する深さを指定する。0だとサブフォルダ内を探索しない。-1だと無限に深く探索する。

```vb
Print GetList(".", 1)
Msgbox "完了"


'ファイル一覧を取得する
Function GetList(sFol, lDepth)
    Dim fso  'ファイルシステムオブジェクト
    Dim fol  'フォルダオブジェクト
    Dim list 'ディクショナリーオブジェクト

    Set fso  = CreateObject("Scripting.FileSystemObject")
    Set fol  = fso.GetFolder(sFol)
    Set list = CreateObject("Scripting.Dictionary")

    Call pr_GetList(fol, lDepth, list)

    GetList = Join(list.Items, vbCrLf) 'ファイル名の一覧を返す
    'GetList = Join(list.keys, vbCrLf) 'ファイルパスの一覧を返す
End Function


'フォルダ毎に呼び出す
Function pr_GetList(fol, lDepth, list)
    Dim f 
    
    For Each f In fol.Files
        'ファイルのパスと名前を格納
        list.Add f.Path, f.Name
    Next
    
    For Each f In fol.SubFolders
        'サブフォルダのパスと名前を格納
        list.Add f.Path, f.Name

        If lDepth <> 0 Then
            'サブフォルダ内を探索する
            Call pr_GetList(f, lDepth - 1, list)
        End If
    Next
End Function


'テキストファイルに出力する
Function Print(str)
    Dim fso
    Dim file

    Set fso = CreateObject("Scripting.FileSystemObject")
    Set file = fso.OpenTextFile("out.txt", 2, True)
    file.Write str
    file.Close
End Function
```

なおフォルダ内のファイル一覧を取得するだけなら、VBScriptを使わなくてもコマンドプロンプトから
`dir /B >> out.txt`とすれば簡単に取得できる。
