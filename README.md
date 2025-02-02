# Regional Prompter
![top](https://github.com/hako-mikan/sd-webui-regional-prompter/blob/imgs/top.jpg)
- custom script for [AUTOMATIC1111's stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 
- Different prompts can be specified for different regions

- [AUTOMATIC1111's stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 用のスクリプトです
- 垂直/平行方向に分割された領域ごとに異なるプロンプトを指定できます

## update/更新情報
- 75トークン以上を入力できるようになりました
- 共通プロンプトを設定できるようになりました
- 設定がPNG infoに保存されるようになりました
- プリセット機能を追加しました
- support over 75 tokens
- common prompts can be set
- setting parameters saved in PNG info
- preset feature added

日本語解説は[後半](概要)です。

# Overview
Latent couple extention performs U-Net calculations on a per-prompt basis, but this extension performs per-prompt calculations inside U-Net. See [here](https://note.com/gcem156/n/nb3d516e376d7) for details.Thanks to furusu for initiating the idea.

## Usage
This section explains how to use the following image, explaining how to create the following image.  
![sample](https://github.com/hako-mikan/sd-webui-regional-prompter/blob/imgs/sample.jpg)  
Here is the prompt.
```
green hair twintail BREAK
red blouse BREAK
blue skirt
```
setting
```
Active : On
Use base prompt : Off
Divide mode : Vertical
Divide Ratio : 1,1,1
Base Ratio : 
````
This setting divides the image vertically into three parts and applies the prompts "green hair twintail" ,"red blouse" ,"blue skirt" from the top to the bottom.

### Active  
If checked, this extention is enabled.

### Prompt
Prompts for different areas are separated by "BREAK". Enter prompts from the left for horizontal prompts and from the top for vertical prompts.
Negative prompts can also be set for each area by separating them with BREAK, but if BREAK is not entered, the same negative prompt will be set for all areas.

### Use base prompt
Check this if you want to use the base prompt, which is the same prompt for all areas. Use this option if you want the prompt to be consistent across all areas.
When using base prompt, the first prompt separated by BREAK is treated as the base prompt.
Therefore, when this option is enabled, one more BRAKE-separated prompt is required than Divide ratios.

### Base ratio
Sets the ratio of the base prompt; if 0.2 is setted, the base ratio is 0.2. It can also be specified for each region, and can be entered as 0.2, 0.3, 0.5, etc. If a single value is entered, the same value is applied to all areas.

### Divide ratio
If you enter 1,1,1, the area will be divided into three parts (33,3%, 33,3%, 33,3%); if you enter 3,1,1, the area will be divided into 60%, 20%, and 20%. Decimal points can also be entered. 0.1,0.1,0.1 is equivalent to 1,1,1.

### Divide mode
Specifies the direction of division. Horizontal and vertical directions can be specified.

### Use common prompt
If this option enabled, first part of the prompt is added to all part.
```
best quality, 20yo lady in garden BREAK
green hair twintail BREAK
red blouse BREAK
blue skirt
```
If enabled, this prompt is treated as following,
```
best quality, 20yo lady in garden, green hair twintail BREAK
best quality, 20yo lady in garden, red blouse BREAK
best quality, 20yo lady in garden, blue skirt
```
So you need to set 4 prompts for 3 regions. If Use base prompt is also enabled 5 prompts are needed. The order is as follows, common,base, prompt1,prompt2,...

### presets
You can save the setting to presets using preset tab. Presets file located in `web-ui-root/scripts/regional_prompter_presets.csv`. Settiing for last generations is automatically saved to presets: `lastrun`.

# 概要
Latent couple extentionではプロンプトごとにU-Netの計算を行っていますが、このエクステンションではU-Netの内部でプロンプトごとの計算を行います。詳しくは[こちら](https://note.com/gcem156/n/nb3d516e376d7)をご参照ください。アイデアを発案されたfurusu様に感謝いたします。

## 使い方
次の画像の作り方を解説しつつ、使い方を説明します。  
![sample](https://github.com/hako-mikan/sd-webui-regional-prompter/blob/imgs/sample.jpg)  
以下がプロンプトです。
```
green hair twintail BREAK
red blouse BREAK
blue skirt
```
設定
```
Active : On
Use base prompt : Off
Divide mode : Vertical
Divide Ratio : 1,1,1
Base Ratio : 
```
この設定では縦方向に三分割し、上から順にgreen hair twintail ,red blouse ,blue skirtというプロンプトを適用しています。
### Active  
ここにチェックが入っている場合有効化します。

### Prompt
領域別のプロンプト同士はBREAKで区切ります。水平の場合は左から、垂直の場合は上から順にプロンプトを入力します。
ネガティブプロンプトもBREAKで区切ることで領域ごとに設定できますが、BREAKを入力しない場合すべての領域に同一のネガティブプロンプトが設定されます。

### Use base prompt
ベースプロンプトとはすべての領域に共通のプロンプトを使用したい場合チェックを入れます。領域で一貫した場面にしたい場合などは使ってください。
ベースプロンプトを使用する場合、BREAK区切られた最初のプロンプトがベースとして扱われます。

### Base ratio
ベースプロンプトの比率を設定します。0.2と入力された場合、ベースの割合が0.2になります。領域ごとにも指定可能で、0.2,0.3,0.5などと入力できます。単一の値を入力した場合はすべての領域に同じ値が適応されます。

### Divide ratio
領域の広さを指定します。1,1,1と入力した場合、三分割されます(33,3%,33,3%,33,3%)。3,1,1と入力した場合60%,20%,20%となります。小数点でも入力可能です。0.1,0.1,0.1は1,1,1と同じ結果になります。

### Divide mode
分割方向を指定します。水平、垂直方向が指定できます。

### Use common prompt
このオプションを有効化すると最初のプロンプトをすべてのプロンプトに加算します。
```
best quality, 20yo lady in garden BREAK
green hair twintail BREAK
red blouse BREAK
blue skirt
```
このようなプロンプトがあるときに、この機能を有効化すると以下のように扱われます。
```
best quality, 20yo lady in garden, green hair twintail BREAK
best quality, 20yo lady in garden, red blouse BREAK
best quality, 20yo lady in garden, blue skirt
```
よって、3つの領域に分ける場合4つのプロンプトをセットする必要があります。Use base promptが有効になっている場合は5つ必要になります。設定順はcommon,base, prompt1,prompt2,...となります。

### プリセット
設定を保存できます。`web-ui-root/scripts/regional_prompter_presets.csv`に保存されています。最後に生成した設定は自動的に`lastrun`に保存されます。
