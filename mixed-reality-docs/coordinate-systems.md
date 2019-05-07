---
title: 座標系統
description: 用來建置讓您輕鬆工作空間座標系統，常設、 聊天室級別和全球規模混合實境體驗。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: 座標系統、 空間座標系統、 方向、 插入擴充槽級別、 常設-小數位數的空間-調整、 全球規模，360 度，插入擴充槽，常設、 聊天室、 世界、 擴展、 位置、 方向、 固定、 附加檔案、 階段、 錨點、 空間的錨點，世界鎖定、 世界鎖定、 主體鎖定、 主體鎖定範圍中，持續性、 共用、 追蹤遺失，雲端空間的錨點
ms.openlocfilehash: fc76a30895a85ab5ca8396540a82965cc35c494e
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597143"
---
# <a name="coordinate-systems"></a>座標系統

在其核心中，混合實境應用程式的地方[全像投影](hologram.md)在您的世界的外觀和聽起來像是真正的物件。 這牽涉到精確地定位，並指定這些全像投影在世界世界是否其實體空間或虛擬的領域，您已建立的使用者，以有意義的地方。 當這類思考的位置和方向您全像投影或任何其他幾何[視線](gaze.md)光線或[交給位置](gestures.md)，Windows 所提供的各種真實世界座標系統，此幾何可以表示，稱為**空間座標系統**。

<br>

>[!VIDEO https://www.youtube.com/embed/TneGSeqVAXQ]

## <a name="device-support"></a>裝置支援

<table>
<tr>
<th>功能</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens （第 1 代）</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">沈浸式耳機</a></th>
</tr><tr>
<td> <a href="coordinate-systems.md#stationary-frame-of-reference">靜態參考座標系</a></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr><tr>
<td> <a href="coordinate-systems.md#attached-frame-of-reference">附加的畫面格的參考</a></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr><tr>
<td> <a href="coordinate-systems.md#stage-frame-of-reference">階段參考架構</a></td><td style="text-align: center;"> 尚不支援</td><td style="text-align: center;"> 尚不支援</td><td style="text-align: center;"> ✔️</td>
</tr><tr>
<td> <a href="coordinate-systems.md#spatial-anchors">空間的錨點</a></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr><tr>
<td> <a href="spatial-mapping.md">空間對應</a></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

## <a name="mixed-reality-experience-scales"></a>混合的實境體驗標尺

混合的實境應用程式可以廣泛的使用者體驗，從只需要耳機的方向，以完整的全球規模的應用程式與遊戲、 需要空間的對應和空間的錨點的 360 度視訊檢視器的設計：
<br>

| 體驗擴展 | 需求 | 範例體驗 | 
|----------|----------|----------|
|  **僅限方向** |  **耳機方向**（重力對齊） |  360 ° 影片的檢視器 | 
|  **Seated-scale** |  上述 plus**耳機位置**相對於零的位置 |  賽車遊戲或空間模擬器 | 
|  **常設級別** |  上述 plus**階段 floor 原點** |  其中您住擊破和閃躲前方就地的動作遊戲  | 
|  **Room-scale** |  上述 plus**階段界限多邊形** |  拼圖遊戲帶謎題 | 
|  **全球規模** |  **空間的錨點**(而且通常[空間對應](spatial-mapping.md)) |  來自您實際的牆，而這類的敵人遊戲[RoboRaid](https://www.microsoft.com/p/roboraid/9nblggh5fv3j) | 

這些經驗標尺遵循 「 巢狀玩偶 」 模型。 Windows Mixed Reality 這裡的關鍵設計原則是指定的耳機支援建置目標的體驗擴展，以及所有較低的標尺的應用程式：
<br>

| 6DOF 追蹤 | Floor 定義 | 追蹤的 360 ° | 定義的範圍 | 空間的錨點 | 最大的經驗 | 
|----------|----------|----------|----------|----------|----------|
|  否 |  - |  - |  - |  - |  **僅限方向** | 
|  **是** |  否 |  - |  - |  - |  **插入擴充槽** | 
|  **是** |  **是** |  否 |  - |  - |  **釐-轉寄** | 
|  **是** |  **是** |  **是** |  否 |  - |  **常設-360 °** | 
|  **是** |  **是** |  **是** |  **是** |  否 |  **Room** | 
|  **是** |  **是** |  **是** |  **是** |  **是** |  **世界** | 

請注意，參考框架階段尚未支援 HoloLens 上。 HoloLens 上的空間調整應用程式目前必須使用[空間對應](spatial-mapping.md)來尋找使用者的底板及背景牆。

## <a name="spatial-coordinate-systems"></a>空間座標系統

所有的 3D 圖形應用程式使用[笛卡兒座標系統](https://docs.microsoft.com/windows/uwp/graphics-concepts/coordinate-systems)理解的位置和方向呈現虛擬世界中的物件。 這類的座標系統建立 3 個垂直軸，沿著其位置的物件： X、 Y 和 Z 軸。

在 [混合實境](mixed-reality.md)，您的應用程式會理解虛擬和實體的座標系統。 Windows 會呼叫一個座標系統，在真實世界中具有實際意義**空間座標系統**。

空間座標系統表示其座標的值，以公尺為單位。 這表示物件置於 2 個單位位置中任一個的 X，Y 或 Z 軸會顯示除了另一個在混合實境中呈現時的 2 公尺。 這可讓您輕鬆地呈現物件和大規模真實世界的環境。

一般情況下，慣用右手或左手，可以是笛卡兒座標系統。 在 Windows 上的空間座標系統總是右手性，這表示，正 x 軸指向右方，正 y 軸指向上方 （對齊重力） 和正 z 軸點朝向您。

在這兩種類型的座標系統中，正 x 軸指向右側，並指向上方的 y 軸的正值。 差別在於是否正 z 軸點朝或離開您。 您的左側或右側的正 X 方向和 curling 它們的正數 Y 方向中，您可以記住正 z 軸點所指的是指的方向。 拇指指向到或離開您的方向是正數的 z 軸點的座標系統的方向。

## <a name="building-an-orientation-only-or-seated-scale-experience"></a>建立僅限方向或插入擴充槽-小數位數的體驗

全像攝影版的關鍵[轉譯](rendering.md)是您的應用程式檢視變更其全像投影的每個畫面格當使用者移動，以符合其預測的前端影片。 您可以建置**安插擴展體驗**方面會變更至使用者的前端的位置，並使用前端方向**靜態參考座標系**。

某些內容必須忽略前端的位置更新，仍使用固定的所選的標題，且使用者的距離隨時。 主要範例是 360 度的視訊： 因為視訊擷取自單一的固定觀點來看，它就會讓檢視位置，相對於內容、 移動視覺效果，即使使用者看起來必須變更檢視方向。 您可以建置這類**方向專用體驗**使用**附加參考座標系**。

### <a name="stationary-frame-of-reference"></a>靜態參考座標系

提供的靜態參考座標系運作方式，來保留物件的使用者附近的位置盡可能穩定相對於世界裡，同時又能採用使用者的前端的位置中的變更的座標系統。

以插入擴充槽擴展這類體驗中的遊戲引擎[Unity](https://unity3d.com/)，靜態參考座標系是定義為引擎的 「 全球原點。 」 會放置在特定的全局座標的物件來定義其使用那些相同的座標現實世界中的位置使用靜態參考座標系。 內容會保留放在世界中，即使在使用者將逐步引導，就所謂**世界鎖定**內容。

應用程式通常會在啟動時建立一個靜態參考座標系，並使用它在整個應用程式的存留期的座標系統。 為 Unity 中的應用程式開發，您可以直接開始放置相對於原點，會在使用者的初始前端的位置和方向的內容。 如果使用者移至新位置，而且想要繼續其表示縮放體驗，您可以 recenter 世界原點在該位置。

經過一段時間，因為系統會更了解使用者的環境中，它可能會判斷現實世界中各個點之間的距離是短一點或長比先前認為系統。 如果您轉譯靜態參考座標系 HoloLens 使用者超出區域大約遠 5 公尺寬走廊的位置上的應用程式在全像投影時，您的應用程式可能會發現漂移中觀察到這些全像投影的位置。 如果您的體驗有超過 5 公尺自己的使用者，您要建置[全球級別的經驗](#building-a-world-scale-experience)，將會需要額外的技術，以保留全像投影穩定，如下所述。

### <a name="attached-frame-of-reference"></a>附加的畫面格的參考

附加的畫面格的參考會隨之移動使用者他們逐步解說，標題為固定的應用程式會先建立框架時所定義。 這可讓使用者舒服地看一下在放內參考該框架的內容。 此使用者相關的方式呈現的內容會呼叫**主體鎖定**內容。

當耳機無法找出其所處的世界中時，附加的畫面格的參考會提供唯一的可用來呈現全像投影的座標系統。 這讓它很適合用於顯示後援的 UI，以告訴他們的裝置中找不到它們世界各地的使用者。 插入擴充槽級別或更高版本的應用程式應包含專用方向的後援，以協助使用者開始同樣地，使用 UI 中顯示的類似[首頁的混合實境](navigating-the-windows-mixed-reality-home.md)。

## <a name="building-a-standing-scale-or-room-scale-experience"></a>建置常設-小數位數或聊天室擴展經驗

在沉浸式耳機超越插入擴充槽擴展和建置**常設擴展經驗**，您可以使用**階段參照**。

提供**聊天室擴展經驗**，讓使用者四處巡察預先定義的 5 公尺界限內，您可以檢查**階段界限**也。

### <a name="stage-frame-of-reference"></a>階段參考架構

當第一次設定沈浸式耳機，使用者會定義**階段**，表示他們將會經歷的聊天室混合實境。 階段會進行最低限度定義**暫置原始**，floor 位置和他們想要使用裝置的其中的正向方向，置於使用者空間座標系統的選擇。 將內容放在 y=0 floor 平面在這個階段座標系統中，您可以確保您全像投影增至地板上時顯示為固定的使用者，而且為使用者提供**常設擴展經驗**。

### <a name="stage-bounds"></a>階段界限

使用者可能也可以選擇性地定義**階段界限**，它們已被清除的家具它們要在中四處移動房間內的區域混合實境。 因此，可以建立應用程式，如果**聊天室擴展經驗**，使用這些界限，以確保全像投影會一律放使用者可以達到。

參考框架階段提供單一固定在其中放置 floor 相對於內容的座標系統，因為它是移植的常設規模和空間規模的應用程式開發的虛擬實境耳機的最簡單路徑。 不過，因為這些 VR 平台，在單一的座標系統可以只穩定有關 5 名計量 （16 英尺） 直徑的內容中，推桿 arm 之前效果會導致遠離 「 管理中心 」 以明顯轉移，因為系統會調整的內容。 要超越遠 5 公尺，所需空間的錨點。

## <a name="building-a-world-scale-experience"></a>建置全球規模的體驗

True 可讓 HoloLens**全球級別體驗**，可讓使用者走廊超過 5 公尺。 若要建置的世界級應用程式，您將需要超出所使用的空間調整體驗的新技術。

### <a name="why-a-single-rigid-coordinate-system-cannot-be-used-beyond-5-meters"></a>為什麼在單一固定的座標系統不能超過 5 公尺

現在，當撰寫遊戲、 資料視覺效果應用程式，或是虛擬實境應用程式，一般的方法並建立所有其他的座標可以可靠地將對應至的一個絕對的全局座標系統。 在該環境中，您一定可以找到穩定的轉換，可定義在這個世界中任何兩個物件之間的關聯性。 如果您未移動這些物件，其相對的轉換會一律保持相同。 轉譯純虛擬世界，其中您所有的幾何事先知道時，就會運作此種類型的全域座標系統。 聊天室擴展 VR 應用程式時，立即通常建立這種絕對的房間擴展地板上其來源的座標系統。

相較之下，例如 HoloLens untethered 混合的實境裝置具有動態感應器導向的了解世界中，調整其知識持續一段時間的使用者的恍神他們逐步許多計量解說跨整個建置的樓層。 在全球級別的經驗中，若您在單一固定座標系統中，所有您全像投影這些全像投影會一定漂移經過一段時間，相對於世界或彼此。

比方說，耳機可能目前認為是 4 個計量，世界中的兩個位置，然後稍後再精簡該了解，學習位置實際上相差 3.9 計量。 如果這些全像投影一開始加入了 4 個計量相隔的單一固定的座標系統，其中會然後一律出現 0.1 公尺關閉，在現實世界中。

### <a name="spatial-anchors"></a>空間的錨點

Windows Mixed Reality 解決讓您建立在上一節中所述的問題[空間的錨點](spatial-anchors.md)來標記使用者已在其中放置全像投影的世界中的重點。 空間的錨點表示系統應該追蹤的一段時間的世界中很重要的一點。

裝置會了解世界，因為這些空間的錨點可以調整它們彼此之間相對的位置，視需要以確保每個錨點保持精確地說從相對於實際的放置方式。 藉由將空間的錨點放在使用者對雷射的放置的位置，並接著定位該全像相對於其空間的錨點，您可以確保全像維護最佳穩定性，即使隨著使用者漫遊跨數十個計量。

這項持續調整空間的錨點，相對於另一個是 coordinate systems 從空間的錨點和 「 定態的參考框架之間的主要差異：

* 全像投影放在靜態參考座標系所有保留另一個固定關聯性。 不過，隨著使用者遠距離，該畫面格的座標系統可能會漂移相對於世界，以確保全像投影之使用者旁邊會出現在穩定。

* 全像投影放在參考框架階段也會保留另一個固定關聯性。 相較於 「 定態的框架中，階段框架一定會保持固定在相對於其定義的實體原點的位置。 不過，轉譯到其 5 公尺界限之外的階段的座標系統中的內容才會出現穩定而使用者釐該界限內。

* 放置於使用空間的錨點可能漂移相對於全像投影的其中一種全像投影放使用另一個空間錨點。 這可讓 Windows 來改善其了解每個空間的錨點的位置，即使，比方說，一個錨點必須調整保留本身，而另一個錨點需要調整權限。

相較於 「 定態畫面格的參考，一律會最佳化的使用者附近的穩定性，階段參考框架和空間的錨點，請確定其來源附近的穩定性。 這可協助保持精確地就地經過一段時間，這些全像投影，但這也表示全像投影從其座標系統的原點太遠而轉譯會發生越來越嚴重推桿 arm 效果。 這是因為更明顯的位置和方向的階段或錨點稍微調整比例從該錨點的距離。 

好的經驗法則是為了確保任何您轉譯遠距空間錨點的座標系統為基礎，是在大約 3 公尺的原始來源。 附近的階段原點，呈現較遠的內容會是 [確定]，因為任何更高的位置錯誤將影響只有小型全像投影，不會轉移大部分的使用者檢視。

### <a name="spatial-anchor-persistence"></a>空間的錨點的持續性

空間的錨點也可以允許您的應用程式，即使之後會暫止您的應用程式或裝置已關閉，請記住重要的位置。

您可以將儲存到磁碟空間的錨點會建立您的應用程式，並再載入回稍後再藉由保存到您的應用程式**空間的錨點存放區**。 當儲存或載入錨點時，會提供字串索引鍵有意義的應用程式，以便日後識別錨點。 這個索引鍵視為錨點的檔案名稱。 如果您想要該錨點相關聯的其他資料，例如使用者放在該位置的 3D 模型、 儲存到您的應用程式的本機儲存體，並將它與您選擇的索引鍵關聯。

您的使用者可以將個別全像投影或將它們所預期的位置，透過許多用途，您的應用程式工作區周圍應用程式會將其各種全像投影，並找出這些全像稍後投影保存至存放區的起點。

您也可以使用<a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空間的錨點</a>非同步闀持續性跨 HoloLens、 iOS 和 Android 裝置。  藉由共用持久的雲端空間錨點，多個裝置可以觀察相同的保存全像經過一段時間，即使這些裝置不存在一起在相同的時間。

### <a name="spatial-anchor-sharing"></a>共用空間的錨點

您的應用程式也可以共用即時空間錨點與其他裝置，以便進行即時共用體驗。

藉由使用<a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空間的錨點</a>，您的應用程式可以跨多個 HoloLens、 iOS 和 Android 裝置共用空間的錨點。 擁有呈現雷射，使用相同的空間錨點的每個裝置，所有的使用者會看到全像圖會出現在真實世界中相同的位置。

## <a name="avoid-head-locked-content"></a>避免 head 鎖定的內容

我們強烈建議轉譯標頭鎖定的內容，會保持固定的位置 （例如抬頭顯示器） 顯示中。 一般情況下，前端鎖定內容時感到不舒服的使用者，且不會不會覺得像是他們的世界自然的一部份。

Head 鎖定的內容通常用來取代全像投影所附加至使用者，或放在本身的世界。 例如，[資料指標](cursors.md)應該通常推送到世界裡，自然地調整，以反映的位置和距離下使用者的視線的物件。

## <a name="handling-tracking-errors"></a>處理追蹤錯誤

在例如深色的走廊某些環境下，它可能無法如耳機使用追蹤內到外本身世界會正確找出。 這可能會導致全像投影而不會顯示，或如果不正確地處理，會出現在正確的位置。 現在，我們討論以這種情形的狀況及其對使用者體驗的影響，以及最佳秘訣處理這種情況。

### <a name="headset-cannot-track-due-to-insufficient-sensor-data"></a>耳機無法追蹤因為沒有足夠的感應器資料

某些情況下，不能找出其中耳機是耳機的感應器。 如果房間是暗或感應器係由其線或實際操作，或如果恍神沒有足夠的紋理，這可能會發生。

當發生這種情況時，耳機將無法追蹤其位置不足，無法呈現世界鎖定全像投影的精確度。 您將無法找出其中空間的錨點，「 定態的框架或階段框架是相對於裝置，但您仍然可以轉譯主體鎖定的內容，在附加的畫面格的參考。

您的應用程式應該會告知使用者如何取得位置追蹤回，呈現一些後援主體鎖定內容描述一些秘訣，例如發掘感應器，並開啟多個號誌。

### <a name="headset-tracks-incorrectly-due-to-dynamic-changes-in-the-environment"></a>耳機會不正確地追蹤因為在環境中的動態變更

某些情況下，裝置不能追蹤適當地如果有大量動態變更，在環境中，例如四處跑在聊天室中的許多人。 在此情況下，全像投影似乎跳或因為裝置會嘗試在此動態環境中追蹤本身漂移。 我們建議使用較低的動態環境中的裝置，如果您遇到這種情況。

### <a name="headset-tracks-incorrectly-because-the-environment-has-changed-significantly-over-time"></a>耳機會因為環境已有重大變更，經過一段時間不正確地追蹤

有時候，當您開始使用耳機經過許多變更的環境中 (例如大量移動的家具，牆 hangings 等)，就可以從其原始位置可能會出現偏移某些全像投影。 當使用者在新領域上移動，則先前全像投影也可能會跳周圍。 這是空間的因為不再有系統的了解您，並嘗試重新對應環境，同時嘗試調解聊天室的功能。 在此案例中，建議您鼓勵重新放置全像投影如果它們未出現於預期的位置固定在世界各地的使用者。

### <a name="headset-tracks-incorrectly-due-to-identical-spaces-in-an-environment"></a>耳機會不正確地追蹤由於相同的環境中的空格

有時候，家用或其他的空間可能會有兩個相同的區域。 例如，兩個相同會議室，相同的兩個角區域中，兩個大型的相同海報涵蓋裝置的視野。 在此情況下，裝置可能，有些時候，相同的組件之間感到混淆，並將它們標示為內部表示法相同。 這可能造成全像投影的某些區域，才會出現在其他位置。 裝置可能會啟動遺失通常追蹤，因為已損毀的環境及其內部表示法。 在此情況下，建議您使用您重設系統的環境了解。 請注意，重設對應會導致遺失的所有空間的錨點位置。 這會導致耳機，來追蹤在環境的唯一區域。 不過，如果裝置取得混淆一次相同的區域之間，可能會重新發生問題。

## <a name="see-also"></a>另請參閱
* [GDC 2017 簡報空間座標系統和全像攝影版的轉譯](https://channel9.msdn.com/events/GDC/GDC-2017/GDC2017-008)
* [在 Unity 中的座標系統](coordinate-systems-in-unity.md)
* [DirectX 中的座標系統](coordinate-systems-in-directx.md)
* [空間的錨點](spatial-anchors.md)
* [在混合實境中共用體驗](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure 空間的錨點</a>
* [案例研究-仔細檢查您實際上的漏洞](case-study-looking-through-holes-in-your-reality.md)