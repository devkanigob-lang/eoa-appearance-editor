# Echoes of Aincrad 外見エディタ MOD (Appearance Editor) v1.0

不可逆な「キャラメイク」を、**外見だけ後からやり直せる**ようにするツールです。
レベル・所持品・クエスト進行などのデータには一切触れません（外見データのみ編集）。

- **色**（肌・髪・瞳・衣装）
- **形**（顔パーツ・顔の輪郭・髪型・体型）… 保存 → 再ロードで反映（タイトルへ戻る等)

---

## 必要なもの

1. **Echoes of Aincrad**（Steam / PC版）
2. **UE4SS（Echoes of Aincrad 対応版）**
   Nexus Mods で配布されています（"UE4SS" for Echoes of Aincrad）。
   https://www.nexusmods.com/echoesofaincrad/mods/7

> このMOD単体では動きません。先に UE4SS の導入が必要です。

---

## 導入手順

### 1) UE4SS を導入
ダウンロードした UE4SS の中身（`dwmapi.dll` と `ue4ss` フォルダ）を、ゲームの
```
<Steam>\steamapps\common\Echoes of Aincrad\EchoesofAincrad\Binaries\Win64
```
（`EchoesofAincrad-Win64-Shipping.exe` がある場所）に置きます。

### 2) 本MODを導入
同梱の `AppearanceEditor` フォルダを、次の場所に丸ごとコピーします。
```
...\EchoesofAincrad\Binaries\Win64\ue4ss\Mods\AppearanceEditor
```
最終的にこうなればOKです。
```
ue4ss\Mods\AppearanceEditor\enabled.txt
ue4ss\Mods\AppearanceEditor\Scripts\main.lua
```

### 3) 起動確認
ゲームを起動します。導入に成功していれば、内部ログ
`...\Binaries\Win64\ue4ss\UE4SS.log` に `Appearance Editor v1.0 loaded` と記録されます。

---

## 使い方

操作はすべて **Ctrl + テンキー**。ゲーム画面をクリックしてアクティブにしてから押してください。

| キー | 機能 |
|------|------|
| **Ctrl + テンキー1** | EXPORT：今の外見値を設定ファイルに書き出す（選択肢つき） |
| **Ctrl + テンキー2** | APPLY：設定ファイルの内容をセーブへ書き込む |
| **Ctrl + テンキー3** | COLORS：設定ファイルの色をその場でライブ反映（プレビュー） |
| **Ctrl + テンキー4** | DUMP：現在値をログに表示 |

### 基本の流れ
1. **既存セーブをロードして、自キャラが表示された状態**にする。
2. **Ctrl + テンキー1** を押す。→ 下記に設定ファイルが生成されます。
   ```
   ...\Binaries\Win64\ue4ss\appearance_config.txt
   ```
   （このファイルが「今の外見のバックアップ」も兼ねます）
3. `appearance_config.txt` をメモ帳等で開いて編集します。
   - 各行の `# コメント` に項目の意味、`選択肢:` に選べる番号が書いてあります。
   - 例：`HeadID=32   # 顔の輪郭・頭のベース(顎)  選択肢: 0,1,2,5,...`
   - 色は `R,G,B,A`（0.0〜1.0）。色を反映するには対応する `bDefault...=false` にします。
   - 変えたくない行は削除してOK（現状維持）。
4. **色**を試すなら、ゲームに戻って **Ctrl + テンキー3**。→ その場で色が変わります。
5. 決まったら **Ctrl + テンキー2**（保存）→ **ゲーム内で通常セーブ** → タイトルへ戻って **再ロード**。
   → 顔・輪郭・髪型・体型・色すべてが反映されます。

---

## 主な編集項目

- 顔パーツ：`Eyebrows`(眉) `Eyeline`(目/アイライン) `Pupil`(瞳) `Nose`(鼻)
- 顔の輪郭/頭：`HeadID`（顎ベース＝輪郭）
- 髪型/頭装備：`HeadGearID`
- ほくろ/そばかす：`MoleID` / `FrecklesID`（0=なし）
- 体型：`MeshScale`(全体) `Chest` `Arms` `Belly` `Hips` `Thighs` `Legs` ほか（1.0が標準）
- 色：`SkinColor`(肌) `HairColor1/2/3`(髪) `PupilColor1/2/3`(瞳) `EyeColor` `LipColor`
  `UpperColor*`(上衣) `GlovesColor*`(手袋) `LowerColor*`(下衣) など

---

## 注意・安全について

- **事前にセーブのバックアップ推奨**。セーブは通常ここにあります：
  `%LOCALAPPDATA%\EchoesofAincrad\Saved\SaveGames\SaveData.sav`
  適用前にこのファイルをコピーしておけば、いつでも元に戻せます。
- 本MODは**外見データのみ**を編集します。レベル・所持品・クエスト等は変更しません。
- **「形」はリアルタイムに変わりません**（ゲームの仕様上、保存→再ロードで反映）。色のみライブ反映できます。
- ノートPC等で**テンキーが無い**場合は、`Scripts\main.lua` 末尾の `Key.NUM_ONE`〜`Key.NUM_FOUR` を
  `Key.F1`〜`Key.F4` などに書き換えてください（変更後はゲーム再起動）。
- うまくいかない時は `...\Binaries\Win64\ue4ss\appedit_probe.txt` に動作ログが残ります。

## アンインストール
`ue4ss\Mods\AppearanceEditor` フォルダを削除するだけです（UE4SSごと消す場合は `dwmapi.dll` と `ue4ss` フォルダを削除）。

## 免責
個人利用の範囲でお使いください。セーブ改変に伴うリスクは自己責任でお願いします。
導入前のバックアップを強く推奨します。
