---
title: 印刷樣式
description: 在您的應用程式體驗中提供資訊的重要項目文字。
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality，設計、 樣式、 字型、 印刷樣式、 ui、 ux
ms.openlocfilehash: b4bac35cbc412ec7102748350c2f5c1e236c2f7d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596044"
---
# <a name="typography"></a>印刷樣式

在您的應用程式體驗中提供資訊的重要項目文字。 就像在 2D 螢幕上的印刷樣式，目標是清楚且容易閱讀。 有了混合實境的 3d 外觀，就有機會影響文字和整體使用者體驗更佳的方式。

![HoloLens 中的印刷樣式範例](images/640px-typography-hero2.jpg)<br>
*HoloLens 中的印刷樣式範例*

當我們談論 3D 中的型別時，我們傾向於認為立體、 體積型的 3D 文字。 有些商標設計和一些其他受限應用程式，除了立體的文字通常會降低文字的可讀性。 即使我們 3d 設計體驗，我們使用 2D 類型因為會更清晰且容易閱讀。

HoloLens，在全像投影使用加法類色彩系統為基礎的光線建構型別。 就像其他全像投影，型別可以放在實際環境中可 world 鎖定，而且從任何角度觀察到。 [視差](https://en.wikipedia.org/wiki/Parallax)類型和環境之間的效果也會增加深度經驗。

## <a name="typography-in-mixed-reality"></a>在混合實境中的印刷樣式

在混合實境中的印刷樣式規則是一樣的任何其他地方。 虛擬世界和現實生活中的文字必須是易於閱讀、 可讀性更高。 文字可能會在牆上或重疊，實體物件。 它可以浮動以及數位使用者介面。 不論內容中，我們會套用相同的讀取和辨識的印刷樣式規則。

### <a name="create-clear-hierarchy"></a>建立明確階層

使用不同類型的大小和重量，建置對比和階層。 定義型別遞增，並遵循整個應用程式體驗會提供絕佳的使用者體驗與一致的資訊階層。

![類型 ramp 範例](images/typography-ramp-1000px.jpg)<br>
*類型 ramp 範例*

### <a name="limit-your-fonts"></a>限制您的字型

請避免使用單一的內容中的兩個以上不同的字型系列。 這會中斷 harmony 和一致性的經驗，並讓它更難使用資訊。 在 HoloLens，因為資訊顯示在實際環境中，頂端使用太多的字型樣式會降低體驗。 Segoe UI 是所有 Microsoft 的數位設計的字型。 它會以一致的方式在 Windows Mixed Reality 殼層。 您可以下載 Segoe UI 字型檔案，從[Windows 設計的工具組頁面](https://docs.microsoft.com/windows/uwp/design-downloads/)。

[Segoe UI 字樣的詳細資訊](https://docs.microsoft.com/windows/uwp/design/style/typography)

### <a name="avoid-thin-font-weights"></a>避免細的字型粗細

避免使用淡或 semilight 字型加權 42pt 之下的類型大小，因為精簡型的垂直筆劃會震動並降低以利閱讀。 新式的字型，具有足夠的筆劃粗細正常運作。 比方說，新細明體和 Arial。 非常清晰 HoloLens 中使用規則或粗體加權值

### <a name="color"></a>色彩

在 HoloLens，因為全像投影建構與加總淺系統，白色文字是極高。 您可以找到 [開始] 功能表和應用程式列上的白色文字的範例。 即使也無須後的調色盤的白色文字是 HoloLens 上運作，複雜的實體背景使得類型難以閱讀。 若要為了改善使用者的焦點，並將實體的背景的干擾降到最低，建議使用深色或回彩色的調色盤上的白色文字。

<br>


![我們建議使用深色或彩色後調色盤上的白色文字。](images/typography-whiteonblack2-1000px.jpg)

我們建議使用深色或彩色後調色盤上的白色文字。

<br>


![黑色文字範例](images/640px-typography-textcolors.jpg)

若要使用深色的文字，您應該使用亮後盤子讓它更容易閱讀。 在累加式的色彩系統中，黑色會以透明方式顯示。 這表示您將無法看到回盤子的黑色文字而不需要以顏色標示。

<br>


![黑色文字範例](images/640px-typography-blackonwhite.jpg)

在 UWP 應用程式，例如存放區或設定值，您可以找到黑色文字的範例。

## <a name="recommended-font-size"></a>建議使用的字型大小

![兩種計量會顯示文字的最佳距離。](images/typography-distance-1000px.jpg)

兩種計量會顯示文字的最佳距離。

混合的實境牽涉到 3d 的深度，因為它不一定容易通訊字型的大小。 使用者的緩和的兩種計量會是放置全像投影的最佳距離。 我們可以使用距離這麼做為基礎來尋找最佳的字型大小。

您可能已經想到，我們使用電腦或平板電腦裝置 （通常在 12 – 產生 32pt) 之間的類型大小的 2 公尺的距離看變得很小。 這取決於每個字型的特性，但在一般情況下，建議最小的類型大小，以利閱讀，而不需要筆劃震動是大約 30 pt。 如果您的應用程式應該使用更接近的距離，就可以使用較小的類型大小。 **點大小為基礎的 Unity 3D 文字網格和 UI 文字。如需詳細的度量和縮放比例，請參閱[Unity 中的文字](text-in-unity.md)。**

## <a name="resources"></a>資源
* [Segoe 字型](http://download.microsoft.com/download/1/B/C/1BCF071A-78EE-4968-ACBE-15461C274B61/Segoe%20fonts%20v1705.zip)
* [HoloLens 字型](http://download.microsoft.com/download/3/8/D/38D659E2-4B9C-413A-B2E7-1956181DC427/Hololens%20font.zip)

![HoloLens 字型可讓您使用 Windows Mixed Reality 符號字符](images/300px-hololensmdl2symbols.jpg)

HoloLens 字型可讓您使用 Windows Mixed Reality 符號字符。

## <a name="see-also"></a>另請參閱
* [在 Unity 中的文字](http://holodocsfuture/index.php?title=Text_in_Unity&action=edit&redlink=1)
* [色彩、 光線和材質](color,-light-and-materials.md)