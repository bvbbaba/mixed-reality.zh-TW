---
title: 空間對應設計
description: 有效使用 HoloLens 內空間的對應需要仔細考量許多因素。
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: 對應 Windows Mixed Reality，設計、 空間、 HoloLens、 surface 的重構、 網狀結構
ms.openlocfilehash: d2ddcbf9458769a60cd3ed2871c5f3405c75f10c
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59591195"
---
# <a name="spatial-mapping-design"></a>空間對應設計

有效使用 HoloLens 內空間的對應需要仔細考量許多因素。

## <a name="device-support"></a>裝置支援

<table>
<tr>
<th>功能</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">沈浸式耳機</a></th>
</tr><tr>
<td> 空間對應</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

## <a name="why-is-spatial-mapping-important"></a>空間對應為何如此重要？

空間對應可讓您能夠將物件放入實際的介面。 這有助於在使用者的世界中的錨點物件，並利用真實世界深度提示。Occluding 您全像投影其他全像投影和真實世界物件為基礎，可協助說服使用者，這些全像投影實際上是在其空間。 在空間中浮動或移動的使用者不會覺得有全像投影為 real。 如果可能的話，緩和資料項目的地方。

放置或移動全像投影 （使用一個簡單的預計的方格） 時，以視覺化方式檢視介面。 這可協助使用者知道其中最可以將它們全像投影，而會向使用者顯示是否尚未尚未對應它們嘗試進行全像在那個點。 您可以 「 billboard 項目"朝向使用者如果他們最後到達某個角度的太多。

## <a name="what-influences-spatial-mapping-quality"></a>影響空間對應品質？

為了提供最佳使用者體驗，請務必了解影響 HoloLens 所蒐集的空間的對應資料品質的因素。

資料空間的對應中的錯誤可分成三種類別：
* **漏洞**:遺漏空間的對應資料從實際的介面。
* **Hallucinations**:介面會存在於不存在於現實世界空間的對應資料。
* **偏差**:真實世界的介面，推送或提取優於符合空間的對應資料中的介面。

頻率和這些錯誤的嚴重性，可能會影響數個因素：

* **使用者動作**
   * 使用者透過其環境的移動方式決定程度環境就會掃描，所以使用者可能需要指引以達到良好的掃描。
   * 用於掃描相機提供 70 度圓錐式，從最小 0.8 公尺至 3.1 計量表距離的最大值，從相機中的資料。 真實世界介面只會掃描此欄位的檢視。 請注意，這些值在未來版本中有所變更。
   * 如果使用者永遠不會取得內 3.1 公尺物件然後它就不會掃描。
   * 如果使用者只能檢視來自小於 0.8 計量在距離之間的物件，則不會掃描 （這可避免掃描使用者的手）。
   * 如果使用者永遠不會看起來是往上 （這是相當一般） 然後上限就可能不會掃描。
   * 如果使用者永遠不會看起來背後家具或牆阻擋它們的物件將不掃描。
   * 介面通常時迎面而不是淺層的角度來檢視掃描較高的品質。
   * 如果 HoloLens 的標頭追蹤系統會暫時失敗 （這可能會發生因為快速的使用者動作、 不佳的光源、 保留的背景牆或相機成為討論），這會造成空間的對應資料中的錯誤。 隨著使用者持續四處移動以及掃描其環境時，任何這類錯誤將會更正經過一段時間。

* **介面的資料**
   * 在真實世界的表面上找到的資料差異極大。 這些會影響反映資料因為它們會影響如何紅外線空間對應的品質。
   * 深色的介面可能不會掃描，直到它們更接近到攝影機，因為它們反射較少的光線。
   * 某些介面可能它們反映要掃描任何距離，因此它們會在介面背後，也引進漏洞錯誤位置的介面，有時太少光線暗。
   * 檢視來解決標題，而不從淺層的角度檢視，可能只會掃描特別閃亮的表面。
   * 鏡像，因為它們會產生 illusory 反射的實際空間和介面，會導致漏洞錯誤以及 hallucination 錯誤。

* **場景影片**
   * 空間對應快速適應變更的環境，例如移動的人員或開啟和關閉的門。
   * 不過，空間對應可以只適用於區域中的變更時該區域會清楚地顯示用於掃描觀景窗。
   * 基於這個原因，它可能會落後現實情況下，可能會導致漏洞或 hallucination 錯誤這個調適。
   * 例如，使用者會掃描朋友，並再進行，而 friend 挪出空間。 Friend （hallucination 錯誤） 的 「 準刪除 」 表示會保存空間的對應資料中，直到使用者就會轉變回，並重新掃描釐 friend 其中的空間。

* **光源干擾**
   * 在場景中的紅外線環境可能會影響掃描，例如強式陽光，通過一個視窗。
   * 特別閃亮的表面可能會干擾反彈關閉它們而造成的偏差錯誤燈光掃描附近的介面。
   * 閃亮的表面反映 light 直接回相機可能會干擾附近的空間，導致浮點過程 hallucinations 或延遲和場景動作的調適。
   * 相同房間內的兩個 HoloLens 裝置應該不會干擾另一個，但是五個以上的 HoloLens 裝置的存在可能會造成干擾。

它可能可以避免或解決這些錯誤的部分。 不過，您應該設計您的應用程式，如此使用者就可以達成其目標，即使空間的對應資料中的錯誤。

## <a name="the-environment-scanning-experience"></a>掃描經驗的環境

HoloLens 學習在其環境中的介面，因為使用者會查看它們。 經過一段時間，HoloLens 建置環境的所有觀察到的組件的掃描。 它也會更新掃描，觀察到環境中的變更。 這項掃描會自動將應用程式啟動次數之間保存。

使用空間的對應每個應用程式應該考慮提供 '掃描體驗;'程序，透過此應用程式會引導使用者掃描所需的應用程式正確運作的介面。

![範例中的掃描](images/sr-mixedworld-140429-8pm-00068-1000px.png)<br>
*範例中的掃描*

這項掃描體驗的本質而有所不同大幅取決於每個應用程式的需求而定，但兩個主要原則應該會引導它的設計。

首先，**清除與使用者之間的通訊是主要的考量**。 使用者應該一律留意是否達成應用程式的需求。 它們不在符合時，它應該立即使用者清楚了解為何這種情形，並它們應該快速主導採取適當動作。

其次，**應用程式應該嘗試之間的效率和可靠性的平衡**。 時若要這樣做可能**可靠地**，應用程式應該會自動分析資料空間對應到儲存使用者的時間。 不是無法可靠地，當應用程式應該改為讓使用者快速提供它所需要的其他資訊給應用程式。

為了協助設計掃描體驗的權限，請考慮下列可能原因通常適用於您的應用程式：

* **沒有掃描的經驗**
   * 應用程式可能會完美地運作，而不需要任何引導式的掃描體驗;它將會了解自然的使用者移動的過程中觀察到的表面。
   * 比方說，讓使用者可以在使用全像攝影版 spraypaint 表面上繪製應用程式需要只知識目前顯示給使用者介面。
   * 環境可能會完全掃描已在其中使用者已花了很多時間使用 HoloLens 一個。
   * 請記住不過相機使用的空間對應可以只看到 3.1 m 前面的使用者，因此空間對應不會知道任何更遠距表面除非使用者已在過去接近距離它們觀察。
   * 讓使用者了解已掃描之表面，應用程式應該提供此效果的視覺化回饋，例如轉換到已掃描的表面上的虛擬 shadows 可協助使用者將全像投影放在這些介面。
   * 在此情況下，空間介面觀察者的週框的磁碟區應該是主體鎖定更新每個框架[空間座標系統](coordinate-systems.md)，如此一來，它們會遵循使用者。

* **找到合適的位置。**
   * 應用程式可能會專用於特定需求的位置。
   * 比方說，應用程式可能需要使用者周圍的空白區域，因此它們可以安全地練習全像攝影版是一隻-fu。
   * 應用程式應該通訊事前完成，使用者任何特定的需求，並強化其清除視覺回應。
   * 在此範例中，應用程式應該以視覺化方式檢視所需的空白區域的範圍，並以視覺化方式反白顯示任何不想要的物件，此區域內存在。
   * 在此情況下，空間介面觀察者的週框的磁碟區應該使用全球鎖定[空間座標系統](coordinate-systems.md)中選擇的位置。

* **找到適合的組態的介面**
   * 應用程式可能需要特定組態介面，例如兩個很大，一般，相反建立鏡像全像攝影版 hall 的背景牆。
   * 在此情況下應用程式必須分析空間的對應，以偵測適當的介面，並直接向這些使用者所提供的介面。
   * 如果應用程式的面分析不完全可靠，使用者應該有的後援選項。 例如，如果應用程式不正確地識別為一般的牆門廊，使用者需要簡單的方式，若要更正這個錯誤。

* **掃描環境的一部分**
   * 應用程式可能想要只擷取環境的組件中，使用者的指示。
   * 比方說，應用程式掃描聊天室的一部分，因此使用者可能會張貼他們想要賣家具的全像攝影版的分類廣告。
   * 在此情況下，應用程式應該擷取使用者性掃描期間所觀察到的區域內的空間的對應資料。

* **掃描整個房間**
   * 應用程式可能需要掃描所有在目前的房間內，包括使用者背後的介面。
   * 例如，遊戲可能將使用者放在 Gulliver，來自數百個接近往所有方向從小型 Lilliputians 圍攻的角色。
   * 在這種情況下，應用程式必須判斷多少的介面，在目前的聊天室已掃描，並導向使用者的視線填寫顯著差距。
   * 此程序的關鍵提供視覺化回應，使它清除至使用者之表面未經掃描。 例如無法使用應用程式[距離為基礎的霧](https://msdn.microsoft.com/library/windows/desktop/bb173401%28v=vs.85%29.aspx)以視覺方式醒目提示未涵蓋的空間對應介面的區域。

* **建立環境的初始快照集**
   * 應用程式可能想要忽略 'snapshot' 的初始內容後的環境中的所有變更。
   * 這可能是環境的適當避免中斷使用者建立的資料緊密結合的初始狀態。
   * 在此情況下，應用程式應該建立一份空間的對應資料處於其初始狀態後的掃描已完成。
   * 應用程式應該繼續接收更新空間對應的資料，如果全像投影仍會正確阻擋環境。
   * 空間對應資料的持續的更新也可讓視覺化任何曾經變更過，釐清使用者先前和目前狀態的環境之間的差異。

* **建立使用者起始的環境的快照集**
   * 應用程式可能只想要回應環境變更時由使用者指示。
   * 比方說，使用者也可以建立多個 3D '雕像' 的朋友，擷取其帶來在不同的時間。

* **允許使用者變更環境**
   * 應用程式可能會被設計來回應使用者的環境中的任何變更即時進行。
   * 比方說，繪製簾使用者可能會觸發 '場景變更' 全像攝影版婧矔菛進行另一端。

* **若要避免空間的對應資料中的錯誤的使用者指南**
   * 應用程式可能想要提供指引給使用者，而它們會掃描其環境。
   * 這可協助使用者避免某些類型的[空間的對應資料中的錯誤](spatial-mapping-design.md#what-influences-spatial-mapping-quality)，例如藉由保持遠離 sunlit windows 或鏡像。

一個的其他詳細資料，要注意的是 'range' 的空間的對應資料不是無限制。 儘管空間的對應會建立永久的大型空間資料庫，它只會使該資料提供給應用程式在各地使用者的有限規模 '泡泡'。 因此如果您開始在開始長辦公室角落，並在遠離開始時，得夠小，則最終打頭陣，空間的介面就會消失。 您當然可以減輕這藉由快取您的應用程式中的這些介面，它們都已消失的可用空間的對應資料之後。

## <a name="mesh-processing"></a>網格處理

它可能有助於在介面中偵測常見的錯誤類型和篩選、 移除或修改為適當的空間的對應資料。

請記住，資料就是要盡可能到真實世界介面上，忠實的空間對應，使得任何處理您套用轉換您的介面，不然' ' 的風險。

以下是不同類型的網格處理，您會發現有用的一些範例：

* **漏洞填滿**
   * 如果掃描失敗深的資料所組成的小型物件，它將保留在周圍的介面中的漏洞。
   * 漏洞會影響阻擋： 全像投影可以看到 '到' 應該不透明的真實世界介面中的漏洞。
   * 漏洞會影響 raycasts： 如果您正使用 raycasts 來協助使用者呈現與互動，它可能不適合通過漏洞這些光線。 一個緩和策略是使用多個 raycasts 涵蓋的適當大小的區域的組合。 這可讓您篩選 '極端值' 的結果，以便即使一個 raycast 通過一個小型的漏洞，彙總的結果仍是有效。 不過，請注意這種方法是在計算成本。
   * 漏洞會影響物理衝突： 可能會透過最低限度值中的一個洞卸除物理模擬所控制的物件，並將其消失不見。
   * 就能夠以填滿介面網狀結構中的這類漏洞。 不過，您將需要微調您的演算法，讓視窗和放這類的 「 真實漏洞 」 執行不會有值。 它可能很難可靠地區分 「 實際漏洞 」 從 「 假想漏洞 」，因此您必須要試驗不同的啟發學習法，例如 'size' 和 '界限形狀'。

* **Hallucination 移除**
   * 反射亮燈，移動的物件可能會讓小型延遲 'hallucinations' 在過程中浮動。
   * Hallucinations 影響阻擋： hallucinations 可能會顯示為深色的圖案，前面的移動和 occluding 其他全像投影。
   * Hallucinations 影響 raycasts： 如果您正使用 raycasts 來協助使用者呈現與互動，這些光線，可能會發生 hallucination，而不是其背後的介面。 如同漏洞，一個緩和策略是使用許多 raycasts 而不是單一的 raycast，但一次這將會出現在計算成本。
   * Hallucinations 影響物理衝突： 物理模擬所控制的物件可能會卡在針對 hallucination，且無法移動的表面上清除區域的空間。
   * 就可以篩選這類 hallucinations 從介面的網狀結構。 不過，如同漏洞，您必須調整您的演算法，讓實際的小型物件，例如 lamp 代表和機門控制代碼執行無法移除。

* **平滑處理**
   * 空間對應可能會傳回似乎是粗糙或 '雜訊' 相較於真實世界與其的介面。
   * 平滑影響物理衝突： 如果粗略最低限度值，實際模擬的 golf 球可能不會回復順暢地跨越它是以直線。
   * 平滑會影響呈現： 粗略的曲面法線會直接視覺化介面，如果可能會影響它的外觀，而且會中斷 [清除] 的外觀。 就可以緩解這個情況的著色器，用來呈現在介面中使用適當的光線和材質。
   * 可以平滑粗糙度介面網狀結構中。 不過，這可能會推送與對應的真實世界介面在進一步的介面。 維護關閉對應是一定要以產生精確的全像阻擋，並讓使用者能夠達到精準且可預測互動全像攝影版的介面。
   * 如果只需要外觀變更時，可能不足以平滑頂點法線，而不需要變更頂點位置。

* **平面尋找**
   * 有許多形式的應用程式可能會想要執行空間對應所提供的介面上的分析。
   * 一個簡單的範例是 '平面尋找';識別繫結，大部分是平面的表面區域。
   * 平面的區域可用來當做全像攝影版工作-平面，全像攝影版的內容可以自動放置應用程式的區域。
   * 平面區域可以限制使用者介面，引導使用者進行互動最符合需要的介面。
   * 平面區域可以用於真實世界中，如同全像攝影版的對應項目，例如 LCD 螢幕、 資料表或白板功能的物件。
   * 平面區域可以定義 play 領域，形成 videogame 層級的基礎。
   * 平面區域可協助虛擬的代理程式，以瀏覽真實世界中，找出實際的人都可能會在逐步引導的樓層的區域。

## <a name="prototyping-and-debugging"></a>原型設計和偵錯

### <a name="useful-tools"></a>有用的工具
* [HoloLens 模擬器](using-the-hololens-emulator.md)可用來開發使用空間的對應，而不需要存取實體的 HoloLens 的應用程式。 它可讓您模擬在實際環境中的 HoloLens 上即時工作階段，所有資料的應用程式會正常取用，包括 HoloLens 影片、 空間座標系統和網路空間的對應。 這可用來提供可靠、 可重複輸入，可用於偵錯的問題及評估您的程式碼的變更。
* 若要重現某些情況下，透過網路從即時的 HoloLens，擷取空間對應的資料，然後將它儲存到磁碟，並在後續的偵錯工作階段中重複使用。
* [Windows 裝置入口網站，3D 檢視](using-the-windows-device-portal.md#3d-view)可用來查看所有透過空間的對應系統目前可用的空間介面。 這會提供您的應用程式; 內的空間介面比較基礎比方說您可以輕易地分辨空間表層。 是否遺失或顯示在錯誤的位置。

### <a name="general-prototyping-guidance"></a>一般的原型設計指引
* 因為[錯誤](spatial-mapping-design.md#what-influences-spatial-mapping-quality)空間的對應中的資料可能強烈影響您的使用者體驗，我們建議您在各種不同的環境中測試您的應用程式。
* 未取得陷入採用總是不斷在相同的位置，例如您在書桌前測試。 請務必測試在不同的位置、 形狀、 大小和資料的各種介面上。
* 同樣地，綜合或記錄資料可用於偵錯，而不會太依賴相同的幾個測試案例。 這可能會延遲尋找多個不同測試已捕捉到稍早的重要問題。
* 最好進行測試與實際 （以及在理想情況下未 coached） 的使用者，因為它們不可能完全相同的方式，您在使用 HoloLens 或您的應用程式。 事實上，它可能會令您吃驚如何分歧人的行為、 知識和假設可以 ！

## <a name="see-also"></a>另請參閱
* [聊天室掃描視覺效果](room-scan-visualization.md)
* [空間完善的設計](spatial-sound-design.md)
* [在 Unity 中的持續性](persistence-in-unity.md)