---
title: 游標
description: 目標向量的游標或指標會提供持續的意見反應，讓使用者瞭解 HoloLens 瞭解其意圖。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens （第1代），HoloLens 2，混合現實，游標，目標，注視，手勢
ms.openlocfilehash: 969906cb09e100dbdd289d78baba722a4bd32537
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723237"
---
# <a name="cursors"></a>游標

![游標](images/UX/UX_Hero_Cursor.jpg)

您目前目標向量的游標或指標，可提供持續的意見反應，讓使用者瞭解耳機在該時間的目前焦點。 游標可讓使用者瞭解其目前的目標點並做為意見反應，以指出哪些區域、全息影像或點將回應輸入。 此數位代表裝置瞭解使用者注意的位置（不過，這可能不會與決定其意圖的任何內容一樣）。

資料指標所提供的意見可讓使用者預測系統的回應方式、使用該信號作為意見反應，以更適當地將其意圖傳達給裝置，最後更有把握其互動。

有3種類型的資料指標：**手指、光線**和**列印頭**。 這些指標游標在 HoloLens、HoloLens 2 和沉浸式耳機上使用不同的輸入形式。 以下是每一種類型的耳機和互動模型所要使用之資料指標類型的指引。 在混合式現實工具組（MRTK）中，我們建立了拖放資料指標模組，協助您建立正確的指標體驗。


## <a name="device-support"></a>裝置支援

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>功能</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (第 1 代)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>沉浸式頭戴裝置</strong></a></td>
    </tr>
     <tr>
        <td>手指游標</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
     <tr>
        <td>光線游標</td>
        <td>❌</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>列印頭游標</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="finger-cursor"></a>手指游標
手指游標僅適用于 HoloLens 2，以加強「[直接操作手](direct-manipulation.md)入」互動模式。 為了進一步瞭解手指指向何處，我們已將環形連接到兩個索引手指的秘訣。 信號大小是以手指與 UI 介面的近距離為基礎（手指越接近，環形越小），當手指與 UI 接觸時，就會縮小為點形狀。 <br>

![手指游標](images/finger-cursor.png)<br>
**手指游標1的視覺意見反應狀態**：環形會縮小為點。 2：環形會與 surface 對齊。 3：環形會與手指向量垂直。 4：無信號。

## <a name="ray-cursor"></a>光線游標
光線游標會附加到最接近的放射處，以允許操作不在手中的物件。 在沉浸式耳機中，光線會從動作控制器開始，並以點游標結束。 在 HoloLens 2 中，我們運用了這些運動控制器光線的心理模型，並設計出來自手掌和結尾的光線，而這些資料指標與直接操作中使用的手指游標一致。 <br>
:::row:::
    :::column:::
        ![光線資料指標控制器](images/ray-cursor-controller.png)<br>
        **動作控制器的光線游標**<br>
    :::column-end:::
    :::column:::
        ![光線游標手](images/ray-cursor-hand.png)<br>
        **手的光線游標**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="head-gaze-cursor"></a>列印頭游標
前端游標是一個點，它會附加至不可見的標頭注視向量的尾端，而這會使用標頭的位置和旋轉。 若要執行動作，此指標會與各種認可輸入配對，例如空中碰、語音命令、停留和按下按鈕。 在 HoloLens 2 中，列印頭最適合與任何不是按下的認可輸入配對，因為在空中點與目前的手片之間會發生互動衝突。 <br>
:::row:::
    :::column:::
        ![Head 注視游標手](images/head-gaze-cursor-hand.png)<br>
        **具有手形手勢的頭部注視游標**<br>
    :::column-end:::
    :::column:::
        ![Head 注視游標語音](images/head-gaze-cursor-voice.png)<br>
        **具有語音命令的頭部注視游標**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="cursor-customization-recommendations"></a>資料指標自訂建議
如果您想要自訂資料指標的意見反應行為和外觀，以下是一些設計建議：

### <a name="cursor-scale"></a>資料指標縮放
* 游標不應大於可用的目標，讓使用者可以輕鬆地與內容互動並加以查看。
* 根據您所建立的經驗，在使用者查看時調整資料指標也是很重要的考慮。 例如，當使用者進一步探討您的經驗時，游標應該不會變得太小，以致遺失。
* 調整游標時，請考慮將軟動畫套用至它，因為它會調整以讓它成為一種有機的感覺。
* 避免阻礙內容。 全像投影是讓體驗更容易記住，而游標不應離開的情況。

### <a name="directionless-cursor-shape"></a>Directionless cursor 圖形
* 雖然沒有一個右資料指標圖形，但我們建議您使用 directionless 圖形，例如圓環。 指向某個方向的游標（例如，傳統箭號游標）可能會讓使用者感到困惑。
* 當使用資料指標將互動指示傳達給使用者時，就會發生例外狀況。 例如，在混合現實 OS 中調整全息影像時，游標會暫時包含箭號，以指示使用者如何移動其手來調整全息形狀。

### <a name="look-and-feel"></a>外觀與風格
* 環圈圖或環圈形的游標適用于許多應用程式。
* 挑選最能代表您所建立之體驗的色彩和形狀。
* 資料指標特別容易[分色](hologram-stability.md#color-separation)。
* 具有平衡之不透明度的小型資料指標會讓它具有資訊，而不會支配視覺階層。
* 請 cognizant 在您的游標後方使用陰影或反白顯示，因為它們可能會妨礙內容，並會與手邊的工作進行干擾。
* 游標應該對齊並在您的應用程式中將介面結合在一起，這會讓使用者覺得系統可以查看他們的外觀，但系統也知道其周圍的環境。 例如，在混合現實的作業系統中，游標會與使用者的世界表面一致，即使使用者不是直接在全息圖上，也能感受到世界的認知。
* 將游標移至接近近近的位置時，會將游標鎖定到互動式元素，有助於改善使用者在執行選取動作時與該元素互動的信心。

### <a name="visual-cues"></a>視覺提示
* 如果您的經驗著重于單一的全息圖形，則您的游標應該只在您離開該全像投影時，才對齊和縮小全像投影和變更形狀。 這可以向使用者傳達可操作的全像投影，而且可以與它互動。
* 如果您的應用程式使用空間對應，則您的游標可以對齊它所看到的每個介面並對其進行結合。 這會對 HoloLens 和您的應用程式可以查看其空間的使用者提供意見反應。 這強調了全息影像在世界各地的真實情況，並協助填補 real 與 virtual 之間的橋樑。
* 瞭解游標在視圖中沒有任何全息影像或表面時應執行的動作。 將它放在使用者前方預先決定的距離，是一個選項。

### <a name="possible-actions"></a>可能的動作
* 游標可以由不同的圖示表示，以傳達可執行檔動作，例如縮放或旋轉。
* 只有在資料指標表示使用者的情況時，才將額外的資訊新增至游標處。 否則，使用者可能不會注意到狀態變更或資料指標混淆。

### <a name="input-state"></a>輸入狀態
* 我們可以使用游標來顯示使用者的輸入狀態或意圖。 例如，我們可以顯示一個圖示，告訴使用者系統看到他們的手上狀態，而且應用程式知道他們已經準備好採取行動。
* 我們也可以使用游標，向使用者顯示系統透過暫時的色彩變更聽到了語音命令

* 下列資料指標狀態可以用不同的方式來執行。 您可以藉由將資料指標模型化，例如狀態機器，來執行這些不同的狀態。 例如：
    * [閒置] 狀態是您在其中顯示預設資料指標的位置。
    * [就緒] 狀態是在您偵測到使用者已準備就緒的位置時。
    * 當使用者執行特定互動時，互動狀態就是。
    * 當您傳達可在全像投影上執行的可能動作時，可能的動作狀態或暫留狀態。

您也可以採用外觀的方式來執行這些狀態，讓您可以在偵測到不同的狀態時顯示不同的藝術資產。

<br>

---


## <a name="going-cursor-free"></a>進入「無資料指標」
當深度的意義是經驗的重要元件，而且當指標互動（透過注視和手勢）不需要精確的精確度時，建議您使用不含資料指標的設計。 系統仍然必須符合資料指標通常符合的需求，方法是提供使用者對其指標的持續意見反應，並協助他們安心地將其意圖傳達給系統。 這可能會透過其他明顯的狀態變更來達成。

<br>

---

## <a name="cursor-in-mrtk-mixed-reality-toolkit-for-unity"></a>適用于 Unity 的 MRTK （混合現實工具組）中的游標
根據預設， [MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)會提供游標 Prefab （[DefaultCursor. prefab](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Cursors)），其具有與 shell 的系統資料指標相同的視覺狀態。 它是在 MRTK 輸入設定檔的 [指標] 下進行指派。 您可以為您的經驗取代/自訂此資料指標。 針對眼睛追蹤輸入的經驗，MRTK 也提供 EyeGazeCursor，其中具有微妙的視覺效果可將干擾降至最低。

* [MRTK - 指標設定檔](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html#pointer-configuration)
* [MRTK - 輸入系統](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)
* [MRTK - 指標](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html)


---

## <a name="see-also"></a>請參閱
* [筆勢](gaze-and-commit.md#composite-gestures)
* [頭部目光和行動](gaze-and-commit.md)
