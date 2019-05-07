---
title: 轉譯
description: 全像攝影版的呈現是否精確地放置在真實世界中，或您已建立的虛擬領域內，可讓您的應用程式在使用者的世界中的確切位置中繪製雷射。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: 轉譯、 全像
ms.openlocfilehash: 9d87af1b445bc6f730dd02bd7bd7f3aefe7f53db
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597014"
---
# <a name="rendering"></a>轉譯

全像攝影版的呈現是否精確地放置在真實世界中，或您已建立的虛擬領域內，可讓您的應用程式在使用者的世界中的確切位置中繪製雷射。 [全像投影](hologram.md)物件提出音效和光線，以及呈現可讓您的應用程式，以新增光線。

## <a name="device-support"></a>裝置支援

<table>
<tr>
<th>功能</th><th style="width:150px"><a href="hololens-hardware-details.md">HoloLens （第 1 代）</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"><a href="immersive-headset-hardware-details.md">沈浸式耳機</a></th>
</tr><tr>
<td>發行項名稱</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr>
</table>

## <a name="holographic-rendering"></a>全像攝影版的轉譯

索引鍵至全像攝影版的轉譯了解您是否要呈現 HoloLens，讓使用者可以看到真實世界和您全像投影一起-例如透明顯示或不透明的顯示，如 Windows Mixed Reality 沈浸式耳機，哪些區塊out 世界。

使用裝置**透明顯示**，例如[HoloLens](hololens-hardware-details.md)，加入世界的光線。 黑色像素會完全透明，但較鮮亮的像素為單位將會越來越不透明。 從顯示的光源加入 light 中，在現實世界中，因為即使白色像素是有點半透明。

立體視覺呈現您全像投影提供一深度提示，新增[紮效果](interaction-fundamentals.md)有助於查看更輕鬆地哪些介面雷射附近的使用者。 接地技術是周圍雷射光暈在附近的介面，並再呈現陰影，以針對這個光暈。 如此一來，要減去光從環境會出現您的陰影。 [空間音效](spatial-sound.md)可以是另一個非常重要的深度提示，讓使用者理解的距離和雷射的相對位置。

裝置**不透明的顯示器**，例如[Windows Mixed Reality 沈浸式耳機](immersive-headset-hardware-details.md)，封鎖世界的配置。 黑色像素會全黑，和任何其他色彩會顯示為該使用者的色彩。 您的應用程式會負責呈現所有項目，使用者會看到，因此它會維護固定的重新整理的頻率，為使用者提供熟悉的體驗更為重要。

## <a name="predicted-rendering-parameters"></a>預測的轉譯參數

混合實境耳機 （包括 HoloLens 和沈浸式耳機） 持續追蹤的位置和方向相對於其周圍環境的使用者的大腦。 當您的應用程式會開始準備其下一個畫面格，系統會預測使用者的大腦是在未來的確切時間擷取的框架將會顯示在顯示器上的位置。 根據這項預測，則系統會計算要用於該範圍內的檢視和投影轉換。 您的應用程式**必須使用這些轉換，才能產生正確結果**; 如果不使用系統提供的轉換，產生的映像不會與現實世界裡，導致使用者 discomfort 一致。

請注意，可以準確地預測新的框架時連線到顯示中，系統會不斷地測量有效的端對端延遲，您的應用程式轉譯管線。 雖然系統會自動調整以轉譯管線的長度，您可以進一步改善全像穩定性保持越短越好該管線。

使用進階的技術來加強系統預測的應用程式可以覆寫的系統檢視和投影轉換。 這些應用程式必須仍然必須使用系統提供的轉換做為其自訂轉換的基礎以產生有意義的結果。

## <a name="other-rendering-parameters"></a>其他轉譯參數

當轉譯畫面格，系統會指定後緩衝區檢視區在其中繪製您的應用程式。 此檢視區通常會比完整畫面格緩衝區的大小還小。 檢視區大小，不論應用程式呈現的畫面格之後便可系統 upscale 要填滿顯示完整的映像。

發現自己無法轉譯需要重新整理速率的應用程式[可以設定系統轉譯參數](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration)來減少記憶體不足的壓力和/或轉譯成本，但是相對地增加的像素的別名。 背景緩衝區格式也可以變更，這對於某些應用程式可以協助改善記憶體頻寬和像素的輸送量。

轉譯範圍、 解析度與畫面播放速率要求呈現您的應用程式可能也會變更框架框架和左邊和右邊的眼睛可能有所不同。 例如，當[混合實境擷取](mixed-reality-capture.md)(MRC) 正在使用中而[相片/影片相機檢視組態](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfigurationKind#Windows_Graphics_Holographic_HolographicViewConfigurationKind)選擇加入，不是一個眼睛可能呈現較大的 FOV 或解析。

針對任何指定框架時，您的應用程式*必須*轉譯使用檢視轉換、 投影轉換，以及系統所提供的檢視區解析。 此外，您的應用程式必須永遠不會假設任何轉譯/檢視參數仍固定從框架至框架中。 引擎，例如 Unity 處理這些所有轉換為您在自己的數位相機物件，以便一律會遵守您的使用者和系統狀態的實體移動。 如果您的應用程式中進一步允許虛擬使用者透過世界 （例如使用搖桿上的遊戲台） 移動，可以新增父"rig 」 物件上方移動，相機造成以反映使用者中的虛擬和實體移動觀景窗。 如果您的應用程式修改檢視轉換、 投影轉換或系統所提供的檢視區維度，它必須通知系統，藉由呼叫適當[覆寫 API](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicCameraPose#Windows_Graphics_Holographic_HolographicCameraPose)。

若要加強的穩定性全像攝影版的轉譯，您的應用程式應該提供給 Windows 每個畫面格深度緩衝區，它用來轉譯。 如果您的應用程式會提供深度緩衝區，它應該有一致的深度值，表示以公尺為單位從相機的深度。 這可讓系統使用每像素深度資料更穩定的內容，如果使用者的大腦最後預測的位置上稍微位移。 如果您不能提供您深度緩衝區，您應該改為提供的焦點所在的位置和標準模式，大部分的內容定義剪下的平面。 如果沒有提供深度緩衝區和焦點平面，系統可能會使用兩者。 特別的是，它可以是來提供深度緩衝區和鶗懘包括速度向量，當您的應用程式，會顯示 「 全像投影中移動時很有幫助。

如需所有低階詳細資料，請參閱[DirectX 中轉譯](rendering-in-directx.md)文章。

## <a name="holographic-cameras"></a>全像攝影版的相機

Windows Mixed Reality 介紹的概念**全像攝影版的相機**。 全像攝影版的數位相機會類似於傳統的觀景窗在 3D 圖形文字中找到： 它們會定義兩個外建 （「 位置 」 和 「 方向 」） 和內建相機屬性 (例如： 欄位的檢視) 用來檢視虛擬的 3D 場景。 不同於傳統的 3D 攝影機、 應用程式不在控制項內的位置、 方向與觀景窗的內建屬性。 相反地，位置和全像攝影版的觀景窗的方向是以隱含方式由控制使用者移動。 使用者的移動轉送上透過檢視轉換以依框架為基礎的應用程式。 同樣地，相機的內建屬性由裝置的校正光學所定義，以及轉送框架逐格透過投影轉換。

一般情況下您的應用程式會轉譯為單一的立體聲相機。 不過，健全的轉譯迴圈應該支援多個數位相機，而且應該支援 mono 和立體聲相機。 比方說，系統可能會要求您的應用程式，來呈現從替代的觀點來看，當使用者啟動的功能，像是[混合實境擷取](mixed-reality-capture.md)(MRC)，根據問題耳機的形狀。 可支援多個相機的應用程式來取得[中選擇](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration)要[種類](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfigurationKind#Windows_Graphics_Holographic_HolographicViewConfigurationKind)相機它們可以支援。

## <a name="volume-rendering"></a>磁碟區轉譯

轉譯醫療時 MRI 或工程 3D 中的磁碟區[磁碟區轉譯](volume-rendering.md)經常使用的技術。 這些技術可以是特別感興趣在混合實境，其中使用者可以自然檢視這類磁碟區從索引鍵的角度，只要移動其標頭。

## <a name="supported-resolutions-on-hololens-1st-gen"></a>HoloLens 上支援的解析度 （第 1 代）
> [!NOTE]
> 將會有更多未來提供這篇文章的更新。 [檢視更新清單](release-notes-april-2018.md)

* 目前和最大支援的解析度是屬性[檢視組態](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration)。 HoloLens 設為 最大解析度，也就是 720p (1268 x 720)，根據預設。
* 最低支援的檢視區大小為 50%的 720p，也就是 360p (為 634 x 360)。 在 HoloLens，這會是 ViewportScaleFactor 為 0.5。
* 任何低於 540 p**不建議使用**visual 降低，因為但可用來識別 bottle necks 中像素的填滿率。

## <a name="supported-resolutions-on-hololens-2"></a>HoloLens 2 上的支援的解決方案

> [!NOTE]
> HoloLens 2 的特定的詳細指引[即將推出](index.md#news-and-notes)。


## <a name="see-also"></a>另請參閱
* [全像穩定性](hologram-stability.md)
* [在 DirectX 中轉譯](rendering-in-directx.md)