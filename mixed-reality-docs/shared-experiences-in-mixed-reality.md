---
title: 混合現實中的共用體驗
description: 全像攝影應用程式可能會在一部 HoloLens 之間共用空間錨點，讓使用者可以在多個裝置上的相同位置呈現全息的全像投影。
author: thetuvix
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: 共用體驗，混合現實，全息影像，空間錨點，多使用者，多個
ms.openlocfilehash: c846bcd8c9c52f1f169d306df3afd4f982656078
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926923"
---
# <a name="shared-experiences-in-mixed-reality"></a>混合現實中的共用體驗

全像投影不需要讓一位使用者保持私用。 全像攝影應用程式可能會在一部 HoloLens、iOS 或 Android 裝置之間共用[空間錨點](spatial-anchors.md)，讓使用者在多個裝置上的相同位置呈現全像投影。

## <a name="six-questions-to-define-shared-scenarios"></a>定義共用案例的六個問題

在您開始設計共用體驗之前，請務必定義目標案例。 這些案例有助於說明您所設計的內容，並建立共同的詞彙，協助比較和對比您的體驗所需的功能。 瞭解核心問題以及解決方案的不同途徑，是發掘這個新媒體的機會的關鍵。

透過我們的 HoloLens 合作夥伴機關的內部原型和探勘，我們建立了六個問題來協助您定義共用案例。 這些問題會形成一個架構，而不是完整的，以協助您提煉案例的重要屬性。

### <a name="1-how-are-they-sharing"></a>1. 他們共用的方式為何？

簡報可能是由單一虛擬使用者引發，而多個使用者可以共同作業，或者老師可能會為使用虛擬材料的虛擬學生提供指引，這種體驗的複雜度會根據使用者擁有的代理人層級而增加。在案例中可能會有。

![Holograph on 資料表的男士和女性](images/man-and-women-with-holograph-on-table-500px.png)

有很多方式可以共用，但我們發現大部分的都屬於三種類別：

* **簡報**：將相同的內容顯示給數個使用者時。 例如：教授會向多名學生提供一個課程，讓他們使用相同的全像攝影材料給所有人。 不過，教授可能會有其他人無法看到的提示和附注。
* 共同**作業：當人員一起合作以**達成一些常見的目標時。 例如：教授會提供一個專案，以瞭解如何執行「心形」外科。 學生會配對並建立共同的技能實驗室經驗，讓醫療學生能夠在核心模型上共同作業並學習。
* **指導**方針：當某位人員正以更多一對一的風格互動來協助他人解決問題時。 例如：當他/她在共用體驗中執行「心形操作」技能實驗室時，專家會提供指引給學生。

### <a name="2-what-is-the-group-size"></a>2. 什麼是群組大小？

**一對一**共用體驗可以提供強式基準，而且在理想的情況下，您可以在此層級建立概念證明。 但是要注意的是，與大型群組共用（超過6個人）可能會導致技術（資料和網路）和社交（在有[數個虛擬人偶](https://vimeo.com/160704056)的房間中的影響）中出現問題。 當您從**小型**到**大型群組**時，複雜性會以指數方式增加。

我們發現群組的需求可以分成三種大小的類別：
* 1:1
* 小型 < 7
* 大型 > = 7

群組大小會產生一個重要的問題，因為它會影響：

* 全像攝影空間中的人員代表
* 物件的縮放比例
* 環境的規模

### <a name="3-where-is-everyone"></a>3. 每個人都是什麼？

當共用體驗發生在相同的位置時，混合現實的強度就會開始進行。 我們稱之為**共置位置**。 相反地，當群組已散發，而且至少有一個參與者不在相同的實體空間（通常是使用 VR 的情況下）時，我們稱之為**遠端體驗**。 通常，您的群組**同時**具有共置和遠端參與者（例如，會議室中的兩個群組）。

![資料表上有三個 holograph 的人員](images/three-people-with-holograph-on-table-500px.png)

下列類別有助於傳達使用者的所在位置：

* **共**置：您的所有使用者都將位於相同的實體空間。
* **遠端**：您所有的使用者都將位於不同的實體空間。
* **兩者**：您的使用者會混合使用共置和遠端空格。

這個問題很重要，因為它會影響：

* 人們如何通訊？
    * 例如：是否應該有虛擬人偶？
* 他們看到的物件。 是否共用所有物件？
* 是否需要調整其環境？

### <a name="4-when-are-they-sharing"></a>4. 他們何時共用？

我們通常會考慮共用的體驗時的**同步**體驗：我們全部都在一起。 但是，如果我們包含一個由他人新增的單一虛擬元素，我們就會有一個**非同步**案例。 想像一下虛擬環境中留下的記事或語音備忘了。 您要如何處理您設計中的100虛擬備忘錄？ 如果是來自具有不同隱私權層級的數十個人，該怎麼辦？

請將您的經驗視為下列其中一種時間：

* **同步**：同時共用全像攝影體驗。 例如：兩個學生同時執行技能實驗室。
* **非同步**：在不同時間共用全像攝影體驗。 例如：兩個學生執行技能實驗室，但在不同的時間使用個別的區段。
* **兩者**：您的使用者有時會同步共用，但其他時間則以非同步方式進行。 例如：一名教授會在稍後為學生執行指派，並在下一天保留學生的筆記。

這個問題很重要，因為它會影響：

* 物件和環境持續性。 例如：儲存狀態，讓它們可以抓取。
* 使用者的觀點。 例如：在離開便箋時，可能會記住使用者所看到的內容。

### <a name="5-how-similar-are-their-physical-environments"></a>5. 它們的實體環境有多相似嗎？

兩個完全相同的真實生活環境（在共置的體驗之外）的可能性是精簡的，除非這些環境已設計為相同。 您更有可能會有**類似**的環境。 例如，會議室很相似，它們通常會有一個集中位置的資料表，並以椅子括住。 另一方面，生活中的房間通常**不同**，而且可以在無限的版面配置陣列中包含任意數目的傢俱。

![資料表上的 Holograph](images/holograph-on-table-500px.png)

請考慮您的分享經驗，並納入這兩個類別的其中一種：

* **類似**：通常會有類似傢俱、環境光線和音效、實體房間大小的環境。 例如：教授在演講廳 A，而學生在演講廳 B 中。上課廳的椅子可能比 B 少，但他們可能會有實體辦公桌來放置全息影像。
* **不同**：傢俱設定、房間大小、光源和音效考慮的環境非常不同。 例如：教授位於焦點房間，而學生位於大型的演講廳，並已填入學生和老師。

請務必[考慮環境](environment-considerations-for-hololens.md)，因為它會影響：

* 人們將如何體驗這些物件。 例如：如果您的體驗在資料表上的效果最佳，而且使用者沒有資料表？ 或是在平面表面上，但使用者有雜亂的空間。
* 物件的縮放比例。 例如：在資料表上放置6英尺的人類模型可能是一項挑戰，但核心模型的效果很好。

### <a name="6-what-devices-are-they-using"></a>6. 他們使用哪些裝置？

今天，您通常會看到兩個[**沉浸式裝置**](immersive-headset-hardware-details.md)之間的共用體驗（這些裝置可能會略有不同的按鈕和相對功能，但不會有太大的差異）**或兩部**全像目標的全像解決方案在這些裝置上。 但請考慮**2d 裝置**（行動/桌面參與者或觀察者）是否為必要的考慮，特別是在**混合2d 和3d 裝置**的情況下。 瞭解您的參與者所使用的裝置類型是很重要的，不只是因為它們有不同的精確度和資料條件約束及機會，但因為使用者對於每個平臺都有獨特的期望。

## <a name="exploring-the-potential-of-shared-experiences"></a>探索共用體驗的潛能

您可以結合上述問題的解答，進一步瞭解您的共用案例，在擴充體驗時 crystallizing 挑戰。 針對 Microsoft 的小組，這有助於建立藍圖來改善我們目前使用的體驗、瞭解這些複雜問題的細微之處，以及如何利用混合現實中的共用體驗。

例如，假設有一個來自 HoloLens 上市的 Skype 案例：使用者已完成[如何修正](https://www.youtube.com/watch?v=iBfzs3G8BEA)損毀的光源，並提供來自遠端的專家的協助。

![透過 Skype for HoloLens 修正光線開關的協助](images/fix-a-broken-switch-with-hololens-640px.jpg)

*專家提供從**2d**、桌上型電腦到**3d、混合現實**裝置使用者的**1:1**指導方針。本**指南**是**同步**的，而實體環境則是**不同**的。*

這種體驗與我們目前的經驗進行了一項變更，也就是將影片和語音的範例套用到新的媒體。 但在未來，我們必須進一步定義案例的機會，以及反映混合現實強度的組建體驗。

請考慮 NASA 的 Jet 推進實驗室所開發的 OnSight 共同作業[工具](https://www.youtube.com/watch?v=XtUyUJAVQ6w)。 使用來自 Mars rover 任務之資料的科學家可以在 Martian 橫向的資料內即時與同事共同作業。

![以遠端方式在不同的同事之間共同作業，以規劃 Mars Rover 的工作](images/onsight-nasa-jpl.gif)

*科學家使用 3d**和 2d**裝置，利用**3d、混合現實**的裝置與一小組較**小**的**遠端**同事探索環境。共同作業是**同步**的（但可透過非同步方式來進行），而實體環境**則是（** 幾乎）**類似**。*

OnSight 之類的體驗會帶來新的共同作業機會。 從實體的角度來看，虛擬環境中的元素會放在同事旁，並在說明其發現時分享其觀點。 OnSight 會使用深度和目前狀態的鏡頭來重新思考在混合現實中的共用體驗。

直覺的共同作業是指交談的探源、一起合作，並瞭解如何將此直覺套用到混合現實的複雜性很重要。 如果我們不能只重新建立混合現實中的共用體驗，但強化它們，就會成為未來工作的架構轉變。 混合現實中的共用體驗設計是嶄新又棒的空間，我們只是一開始就了。

## <a name="get-started-building-shared-experiences"></a>開始建立共用體驗

視您的應用程式和案例而定，會有各種需求來達到您想要的體驗。 其中一些包括：

* 比對：建立會話、公告會話、探索和邀請特定人員（在本機或遠端）以加入**您的會話**的能力。
* **錨點共用**：能夠將座標組齊通用本機空間中的多個裝置，讓所有人都能在相同的位置上顯示全像投影。
* **網路**功能：能夠在所有參與者之間即時同步處理人員的位置、互動和移動。
* **狀態儲存體**：能夠將全息影像特性和位置儲存于中間會話聯結的空間中，稍後再重新叫用，並針對網路問題進行更強大的防護。

共用體驗的關鍵在於，有多個使用者在自己的裝置上看到相同的全息影像，通常是藉由共用錨點來在裝置之間對齊座標而完成。

若要共用錨點，請使用[Azure 空間錨點](https://docs.microsoft.com/azure/spatial-anchors)：

* 首先，使用者會放置全息影像。
* 應用程式會建立[空間錨點](spatial-anchors.md)，以精確地在世界中釘選該全息影像。
* 您可以透過[Azure 空間錨點](https://docs.microsoft.com/azure/spatial-anchors/)，將錨點分享給 HoloLens、IOS 和 Android 裝置。

使用共用空間錨點，每個裝置上的應用程式現在都有[共同的座標系統](coordinate-systems.md)，可以在其中放置內容。 現在，應用程式可以確保在相同位置放置和定位全息影像。

在 HoloLens 裝置上，您也可以從一個裝置離線共用錨點到另一個裝置。  使用下列連結來決定最適合您應用程式的內容。

## <a name="evaluating-tech-options"></a>評估技術選項

有各種服務和技術選項可協助您建立多使用者的混合現實體驗。  選擇路徑可能會很難，因此，請以案例為主的觀點來看，以下是一些選項的詳細說明。

## <a name="shared-static-holograms-no-interactions"></a>共用靜態全息影像（無互動）

在您的應用程式中運用[Azure 空間錨點](https://docs.microsoft.com/azure/spatial-anchors/)。  在裝置上啟用和共用空間錨點，可讓您建立一個應用程式，使用者會在同一時間看到全像位置的全息影像。  需要跨裝置進行額外的同步處理，讓使用者能夠與全息影像互動，以及查看全息影像的移動或狀態更新。

## <a name="share-1st-person-perspective"></a>分享第一個人的觀點

當您擁有支援的 Miracast 接收器（如電腦或電視）時，請將內建的 Miracast 支援運用於本機使用者，而不需要額外的應用程式代碼。

在您的應用程式中、遠端使用者或您想要共用的非 Miracast 裝置上，運用[MixedReality WebRTC](https://github.com/microsoft/mixedreality-webrtc) 。  啟用 WebRTC 連線可讓使用者之間的1:1 音訊/影片串流，以及跨裝置的訊息傳輸資料通道。  混合現實實行會針對 HoloLens 進行優化，方法是提供 HoloLens 使用者觀看的混合現實影片串流給其他人。  如果您想要將影片串流擴充到多個遠端用戶端，通常會使用[MCU 服務提供者](https://webrtcglossary.com/mcu/)（Multipoint 會議單位），例如[SignalWire](https://signalwire.com/)。  您可以透過[Freeswitch](https://github.com/andywolk/azure-freeswitch-gpu-windows)取得對 Azure 的單鍵 SignalWire 部署。

> [!NOTE]
> 請注意，SignalWire 是付費服務，並不是 Microsoft 所擁有/附屬的。

## <a name="presenter-spectator-applications-and-demos"></a>展示者-Spectator 應用程式和示範

利用[MixedReality-SpectatorView](https://github.com/microsoft/MixedReality-SpectatorView)將[spectator view 功能](spectator-view.md)帶入您的應用程式。  啟用其他裝置（HL、Android、iOS 和攝影機），以查看 HoloLens 在相同位置的不同觀點所看到的內容，以及接收與全息影像互動之主機 HoloLens 使用者互動的更新。  使用相同應用程式的 spectator 附屬，觀看、拍照，並錄製主機在應用程式中從您自己的空間中的全像投影所執行之工作的影片。

**注意：** 相片會透過 iOS/Android 裝置上的螢幕擷取畫面來取得。

## <a name="multi-user-collaborative-experience"></a>多使用者協同作業體驗

從我們的[多使用者學習教學課程](mrlearning-sharing(photon)-ch1.md)開始，它會利用本機使用者的[Azure 空間錨點](https://docs.microsoft.com/azure/spatial-anchors/)和[Photon SDK](https://www.photonengine.com/PUN)來同步處理場景中的內容/狀態。 建立在本機共同作業的應用程式，讓每位使用者在場景中的全息影像上有自己的觀點，而且每一個都可以完全與全息影像互動。  在所有裝置上提供更新，而互動衝突管理則是由 Photon 處理。

> [!NOTE]
> 請注意， [Photon](https://www.photonengine.com/)是非 Microsoft 產品，因此可能需要與 Photon 的計費關係，才能 productize 和調整以提供更高的使用量。

## <a name="future-work"></a>未來的工作

元件功能和介面可協助在各種案例和基礎技術上提供通用一致性和健全的支援。  在那之前，請選擇與您嘗試在應用程式中達成的案例相符的最佳路徑。

不同的案例，或想要使用不同的技術/服務？ 請在此頁面底部的對應存放庫中提供意見反應作為 GitHub 問題，或[HoloDevelopers 的時差](https://holodevelopers.slack.com/)。

## <a name="see-also"></a>請參閱

* [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors)
* [DirectX 中的共用空間錨點](shared-spatial-anchors-in-directx.md)
* [Unity 中的共用體驗](shared-experiences-in-unity.md)
* [觀眾檢視](spectator-view.md)
