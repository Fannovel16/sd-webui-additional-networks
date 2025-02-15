## Additional Networks for generating images

日本語の文章は下のほうにあります。

## Updates / 更新情報

__Stable Diffusion web UI now seems to support LoRA trained by ``sd-scripts``.__ Thank you for great work!!!

Note: Currently the models trained by the scripts 0.4.0 and the models for SD 2.x does not seem to be supported in Web UI.

- Jan 24 2023, 2023/1/24:
  - Fix the LoRA model trained with ``sd-scripts`` 0.4.0 for SD2.x is not working.
  - ``sd-scripts`` の0.4.0以降で学習されたSD2.x用のLoRAが正しく動作しない不具合を修正しました。
- Jan 23 2023, 2023/1/23:
  - Fix an error with a model saved with ``bf16`` in .pt or .ckpt format.
     - If you use ``bf16`` with .pt/.ckpt, it seems to be required to disable safe-unpickle temporarily with ``--disable-safe-unpickle`` option for web UI. Please use ``.safetensors`` format for ``bf16``.
  - ``bf16`` で保存された.ptまたは.ckptのモデルが読み込めない不具合を修正しました。
     - これらのモデルをweb UIで読み込むには、``--disable-safe-unpickle`` で一時的にweb UIの safe-unpickle を無効にする必要があるようです。``bf16`` での保存には ``.safetensors`` をお使いください。
- Jan 22 2023, 2023/1/22:
  - Add support for ``sd-scripts`` release 0.4.0. 
    - ``alpha`` value for weights scaling is supported.
    - The models trained by the scripts before 0.4.0 are also supported.
  - Add new metadata.
  - ``sd-scripts`` のバージョン0.4.0に対応しました。
    - 重みを加減する ``alpha`` 値に対応しました。
    - 以前のバージョンで作成したモデルも引き続きサポートされます。
  - いくつかの新しいメタデータを追加しました。

## About

This extension is for [AUTOMATIC1111's Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui), allows the Web UI to add some networks (e.g. LoRA) to the original Stable Diffusion model to generate images. Currently LoRA is supported. The addition is on-the-fly, the merging is not required.

This extension supports the LoRA models (*.ckpt or *.safetensors) trained by our scripts in [sd-scripts](https://github.com/kohya-ss/sd-scripts). The models from other LoRA implementations are not supported.

This extension does not support training.

Other networks other than LoRA may be supported in the future.

## Installation

1. Open "Extensions" tab.
1. Open "Install from URL" tab in the tab.
1. Enter URL of this repo to "URL for extension's git repository".
1. Press "Install" button.
1. Restart Web UI.

## How to use

Put the LoRA models (`*.pt`, `*.ckpt` or `*.safetensors`) inside the `sd-webui-additional-networks/models/LoRA` folder.

Open __"Additional Networks"__ panel from the left bottom of Web UI.

Press __"Refresh models"__ to update the models list.

Select __"LoRA"__ for __"Network module 1"__.

Choose __the name of the LoRA model file__ in __"Model 1"__.

Set __the weight__ of the model (negative weight might be working but unexpected.)

Repeat them for the module/model/weight 2 to 5 if you have other models. Models are applied in the order of 1 to 5.

You can generate images with the model with these additional networks.

## X/Y plot

If you use LoRA models to plot, put the comma separated list of the model names into ``AddNet Model X`` 

![image](https://user-images.githubusercontent.com/52813779/212444037-8ccd9157-c341-4eb4-82b4-64e3c8ee0237.png)

You can get the list in ``Additional Networks`` tab on top of the UI. Select some model from ``Model`` dropdown, and push ``Get List`` button. The model list can be copied for X/Y values.

![image](https://user-images.githubusercontent.com/52813779/212443639-97779d8d-0f7e-47f0-919c-41f053fe28a9.png)

The metadata of the model can be drawn as legends. Move to ``Settings`` tab, select ``Additional Networks`` at left bottom, and set ``Metadata to show``. Available values are in ``Network metadata`` textbox in ``Additional Networks`` tab.

![image](https://user-images.githubusercontent.com/52813779/212443781-1f4c442e-c2f3-47f8-b698-25fbe981f633.png)

## この Web UI 拡張について

LoRA などのネットワークを元の Stable Diffusion に追加し、画像生成を行うための拡張です。現在は LoRA のみ対応しています。

この拡張で使えるのは[sd-scripts](https://github.com/kohya-ss/sd-scripts)リポジトリで学習した LoRA のモデル（\*.ckpt または \*.safetensors）です。他の LoRA リポジトリで学習したモデルは対応していません。

この拡張単体では学習はできません。

将来的に LoRA 以外のネットワークについてもサポートするかもしれません。

## インストール

1. Web UI で "Extensions" タブを開きます。
1. さらに "Install from URL" タブを開きます。
1. "URL for extension's git repository" 欄にこのリポジトリの URL を入れます。
1. "Install"ボタンを押してインストールします。
1. Web UI を再起動してください。

## 使用法

学習した LoRA のモデル(`*.pt`, `*.ckpt`, `*.safetensors`)を`sd-webui-additional-networks/models/LoRA`に置きます。

Web UI の左下のほうの __"Additional Networks"__ のパネルを開きます。

__"Network module 1"__ で __"LoRA"__ を選択してください。

__"Refresh models"__ で LoRA モデルのリストを更新します。

__"Model 1"__ に学習した LoRA のモデル名を選択します。

__"Weight"__ にこのモデルの __重み__ を指定します（負の値も指定できますがどんな効果があるかは未知数です）。

追加のモデルがある場合は 2～5 に指定してください。モデルは 1~5 の順番で適用されます。

以上を指定すると、それぞれのモデルが適用された状態で画像生成されます。

## X/Y plot

LoRAモデルをX/Y plotの値（選択対象）として使う場合は、カンマ区切りのモデルのリストを与える必要があります。

![image](https://user-images.githubusercontent.com/52813779/212444037-8ccd9157-c341-4eb4-82b4-64e3c8ee0237.png)

モデルのリストはWeb UI上部の ``Additional Networks`` タブで取得できます。タブを開き、 ``Model`` ドロップダウンから適当なモデルを選択し、``Get List`` ボタンを押してください。モデルのリストが表示されます。リストはコピーしてX/Y plotのvaluesに指定できます。

![image](https://user-images.githubusercontent.com/52813779/212443639-97779d8d-0f7e-47f0-919c-41f053fe28a9.png)

モデルのメタデータ（学習時のパラメータなど）をX/Y plotのラベルに使用できます。Web UI上部の ``Settings`` タブを開き、左下から ``Additional Networks`` を選び、 ``Metadata to show`` にカンマ区切りで項目名を指定してください（``ss_learning_rate, ss_num_epochs`` のような感じになります）。使える値は ``Additional Networks`` の ``Network metadata`` 欄にある値です。

![image](https://user-images.githubusercontent.com/52813779/212443781-1f4c442e-c2f3-47f8-b698-25fbe981f633.png)

