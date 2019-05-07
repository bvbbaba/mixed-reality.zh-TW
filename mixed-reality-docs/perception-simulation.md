---
title: Perception 模擬
description: 使用認知模擬程式庫來自動化模擬的輸入沉浸式應用程式的指南
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens，模擬測試
ms.openlocfilehash: 693750eb753bd11cbe7d7cfb47e04f1a3506ca9a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595377"
---
# <a name="perception-simulation"></a>Perception 模擬

若要建置應用程式的自動化的測試嗎？ 您想要超越元件層級的單元測試，並確實執行您應用程式端對端測試嗎？ Perception 模擬是您要尋找的內容。 Perception 模擬程式庫傳送假的人們和世界的輸入的資料給您的應用程式讓您可以將自動化測試。 例如，您可以模擬人類尋找左右，然後執行動作的輸入。

Perception 模擬可以傳送如下的模擬的輸入實體的 HoloLens、 HoloLens 的模擬器，或安裝的混合實境入口網站的電腦。 模擬會略過混合實境裝置上的即時感應器並傳送認知模擬裝置上執行的應用程式的輸入。 應用程式收到這些假的輸入的事件，透過相同的 Api，它們一律使用和無法分辨執行搭配真實感應器與 Perception 模擬與執行之間的差異。 Perception 模擬是 HoloLens 模擬器用來傳送模擬的輸入到 HoloLens 虛擬機器中的相同技術。

模擬會藉由建立 IPerceptionSimulationManager 物件開始。 從該物件中，您可以發出命令來控制模擬 「 人 」，包括前端的位置、 游標位置和筆勢的屬性。

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a>Visual Studio 專案設定 Perception 模擬
1. [安裝 HoloLens 模擬器](install-the-tools.md)開發電腦上。 模擬器會包含您要用於 Perception 模擬程式庫。
2. 建立新的 Visual StudioC#桌面 （主控台專案非常適合開始） 的專案。
3. 做為參考，將下列二進位檔加入至專案 (專案]-> [新增...]-> [參考)。您可以找到它們 **%programfiles (x86) %\Microsoft XDE\10.0.11082.0** 。 PerceptionSimulationManager.Interop.dll-管理C#Perception 模擬的包裝函式。
    b. PerceptionSimulationRest.dll-設定 web 通訊端通訊通道的 HoloLens 或模擬器的程式庫。
    c.  SimulationStream.Interop.dll-模擬的共用類型。
4. 將實作新增至您的專案二進位 PerceptionSimulationManager.dll。 第一次以二進位格式將它新增至專案 (專案]-> [新增...]-> [現有項目)。將它儲存為連結，使它不會將它複製到您專案的來源資料夾。 ![加入專案做為連結的 PerceptionSimulationManager.dll](images/saveaslink.png) b。 請確定它取得的複製到組建輸出資料夾。 這是在二進位檔的屬性工作表中。 ![若要複製到輸出目錄的 Mark PerceptionSimulationManager.dll](images/copyalways.png)

## <a name="creating-an-iperceptionsimulation-manager-object"></a>建立 IPerceptionSimulation Manager 物件

若要控制模擬，您將更新發給 IPerceptionSimulationManager 物件中擷取的物件。 第一個步驟是取得該物件，並將它連接到您的目標裝置或模擬器。 您可以在裝置入口網站中的按鈕，即可取得您的模擬器的 IP 位址[工具列](using-the-hololens-emulator.md#anatomy-of-the-hololens-emulator)

![開啟 [裝置入口網站] 圖示](images/emulator-deviceportal.png)**開啟裝置入口網站**:開啟 Windows Device Portal HoloLens os 在模擬器中。

首先，您將呼叫 RestSimulationStreamSink.Create 取得 RestSimulationStreamSink 物件。 這是目標裝置或模擬器，您會控制透過 http 連線。 您的命令將會傳遞至，而且由[Windows Device Portal](using-the-windows-device-portal.md)裝置或模擬器上執行。 您必須建立物件的四個參數如下：
* Uri 的 uri-目標裝置的 IP 位址 (例如，"http://123.123.123.123")
* System.Net.NetworkCredential 認證-使用者名稱/密碼連接到[Windows Device Portal](using-the-windows-device-portal.md)目標裝置或模擬器上。 如果您要連接到其本機 168 透過模擬器。*.*。 * 位址將會在相同電腦上，接受任何認證。
* bool 正常-適用於一般的優先權，則為 false 的低優先順序服務。 您通常想要將此設為 *，則為 true*進行測試案例。
* System.Threading.CancellationToken 權杖-語彙基元來取消非同步作業。

其次，您將建立 IPerceptionSimulationManager。 這是您用來控制模擬的物件。 請注意，這也必須在非同步方法。

## <a name="control-the-simulated-human"></a>控制模擬人類看得

IPerceptionSimulationManager 有一個人為的屬性會傳回 ISimulatedHuman 物件。 若要控制模擬人類看得，執行此物件上的作業。 例如: 

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a>基本範例C#主控台應用程式

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Task.Run(async () =>
            {
                try
                {
                    RestSimulationStreamSink sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("http://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        new System.Threading.CancellationToken());

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();
        }
    }
}
```

## <a name="extended-sample-c-console-application"></a>擴充範例C#主控台應用程式

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Task.Run(async () =>
            {
                try
                {
                    RestSimulationStreamSink sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("http://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        new System.Threading.CancellationToken());

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);

                    // Now, we'll simulate a sequence of actions.
                    // Sleeps in-between each action give time to the system
                    // to be able to properly react.
                    // This is just an example. A proper automated test should verify
                    // that the app has behaved correctly
                    // before proceeding to the next step, instead of using Sleeps.

                    // Simulate Bloom gesture, which should cause Shell to disappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... this time, Shell should reappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate a Head rotation down around the X axis
                    // This should cause gaze to aim about the center of the screen
                    manager.Human.Head.Rotate(new Rotation3(0.04f, 0.0f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a finger press & release
                    // Should cause a tap on the center tile, thus launching it
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate a second finger press & release
                    // Should activate the app that was launched when the center tile was clicked
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(5000);

                    // Simulate a Head rotation towards the upper right corner
                    manager.Human.Head.Rotate(new Rotation3(-0.14f, 0.17f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a third finger press & release
                    // Should press the Remove button on the app
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... bringing the Shell back once more
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();
        }
    }
}
```

## <a name="api-reference"></a>API 參考資料

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a>Microsoft.PerceptionSimulation.SimulatedDeviceType

描述模擬的裝置類型

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**

虛構的參考裝置 PerceptionSimulationManager 的預設值

### <a name="microsoftperceptionsimulationheadtrackermode"></a>Microsoft.PerceptionSimulation.HeadTrackerMode

說明前端的追蹤器模式

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**

追蹤的預設標頭。 這表示系統可能會選取最佳的標頭追蹤執行階段條件所根據的模式。

**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**

方向追蹤了唯一的標頭。 這表示可能不可靠，追蹤的位置，而且可能無法使用某些功能依賴前端的位置。

**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**

位置標頭追蹤。 這表示，追蹤前端的位置和方向都可靠

### <a name="microsoftperceptionsimulationsimulatedgesture"></a>Microsoft.PerceptionSimulation.SimulatedGesture

描述模擬的筆勢

```
public enum SimulatedGesture
{
    None = 0,
    FingerPressed = 1,
    FingerReleased = 2,
    Home = 4,
    Max = Home
}
```

**Microsoft.PerceptionSimulation.SimulatedGesture.None**

用來不表示任何筆勢的 sentinel 值

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**

手指，按下動作

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**

發行的手指筆勢

**Microsoft.PerceptionSimulation.SimulatedGesture.Home**

主要的筆勢

**Microsoft.PerceptionSimulation.SimulatedGesture.Max**

最大的有效筆勢

### <a name="microsoftperceptionsimulationplaybackstate"></a>Microsoft.PerceptionSimulation.PlaybackState

描述播放狀態

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

**Microsoft.PerceptionSimulation.PlaybackState.Stopped**

錄製目前處於已停止，可以開始播放

**Microsoft.PerceptionSimulation.PlaybackState.Playing**

目前正在播放錄製

**Microsoft.PerceptionSimulation.PlaybackState.Paused**

目前已暫停錄製

**Microsoft.PerceptionSimulation.PlaybackState.End**

記錄已到達結尾

### <a name="microsoftperceptionsimulationvector3"></a>Microsoft.PerceptionSimulation.Vector3

說明 3 個元件的向量，可能會說明了點或在 3D 空間中的向量

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

**Microsoft.PerceptionSimulation.Vector3.X**

向量的 X 元件

**Microsoft.PerceptionSimulation.Vector3.Y**

向量的 Y 元件

**Microsoft.PerceptionSimulation.Vector3.Z**

向量的 Z 元件

**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**

建構新的 Vector3

參數
* x 軸向量的 x 元件
* 向量的 y y 元件
* 向量的 z z 元件

### <a name="microsoftperceptionsimulationrotation3"></a>Microsoft.PerceptionSimulation.Rotation3

描述的 3 個元件的旋轉

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

**Microsoft.PerceptionSimulation.Rotation3.Pitch**

輪替的字幅元件向下繞著 X 軸

**Microsoft.PerceptionSimulation.Rotation3.Yaw**

向右繞著 Y 軸旋轉的繞的元件

**Microsoft.PerceptionSimulation.Rotation3.Roll**

向右繞著 Z 軸旋轉的向前復原的元件

**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**

建構新的 Rotation3

參數
* 字距-旋轉的字幅元件
* 繞-旋轉的繞元件
* 向前復原-旋轉的彙總元件

### <a name="microsoftperceptionsimulationfrustum"></a>Microsoft.PerceptionSimulation.Frustum

描述檢視範圍，通常由相機

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

**Microsoft.PerceptionSimulation.Frustum.Near**

位在範圍中包含的最小距離

**Microsoft.PerceptionSimulation.Frustum.Far**

包含位在範圍中最大距離

**Microsoft.PerceptionSimulation.Frustum.FieldOfView**

水平視野的範圍，以弧度為單位 （大於或等於 PI）

**Microsoft.PerceptionSimulation.Frustum.AspectRatio**

水平視野來檢視垂直欄位的比率

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.IPerceptionSimulationManager

產生用來控制裝置的封包的根

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**

擷取解譯模擬的人類和模擬的世界的模擬的裝置物件。

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**

擷取控制模擬人類看得的物件。

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**

模擬重設為其預設狀態。

### <a name="microsoftperceptionsimulationisimulateddevice"></a>Microsoft.PerceptionSimulation.ISimulatedDevice

描述可解譯模擬的世界和模擬裝置的介面

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**

從模擬裝置中擷取的標頭追蹤器。

**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**

擷取從模擬裝置的手動追蹤程式。

**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**

設定模擬的裝置，以符合所提供的裝置類型的屬性。

參數
* 類型-新的模擬裝置類型

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a>Microsoft.PerceptionSimulation.ISimulatedHeadTracker

描述追蹤模擬人類的標頭的模擬裝置的部分介面

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**

擷取並設定目前的前端的追蹤器模式。

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a>Microsoft.PerceptionSimulation.ISimulatedHandTracker

描述追蹤的模擬人類的模擬裝置的部分介面

```
public interface ISimulatedHandTracker
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    float Pitch { get; set; }
    bool FrustumIgnored { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    Frustum Frustum { get; set; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**

擷取與世界相關節點的位置，以公尺為單位

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**

擷取和設定模擬的手動追蹤器的位置相對於標頭的中心。

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**

擷取和設定模擬的手動追蹤器的向下的字幅

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**

會擷取和設定是否會忽略模擬的手動追蹤器的範圍。 當被忽略，雙手永遠會顯示。 不忽略 （預設值） 時手才看得到它們時手動追蹤器的範圍內。

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**

擷取並設定用來判斷是否模擬的手動追蹤器看到實際操作的範圍屬性。

### <a name="microsoftperceptionsimulationisimulatedhuman"></a>Microsoft.PerceptionSimulation.ISimulatedHuman

上方的層級介面來控制模擬人類看得

```
public interface ISimulatedHuman 
{
    Vector3 WorldPosition { get; set; }
    float Direction { get; set; }
    float Height { get; set; }
    ISimulatedHand LeftHand { get; }
    ISimulatedHand RightHand { get; }
    ISimulatedHead Head { get; }
    void Move(Vector3 translation);
    void Rotate(float radians);
}
```

**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**

擷取和設定節點的位置與相關的世界裡，以公尺為單位。 位置相對應的人力英呎的中心點。

**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**

擷取，並在世界中設定模擬的人臉的方向。 0 的弧度為單位，面臨下負 Z 軸。 正數的弧度順時針旋轉繞 Y 軸。

**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**

擷取和設定的高度，模擬的人，以公尺為單位

**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**

擷取模擬人類看得在左邊

**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**

擷取的模擬人類看得右下

**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**

擷取標頭的模擬人類看得

**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**

移動模擬人類看得相對於其目前的位置，以公尺為單位

參數
* 轉譯-若要移動，相對於目前的位置轉譯

**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**

旋轉模擬的人類相對於其目前的方向，順時針方向繞 Y 軸

參數
* 弧度為單位-要繞著 Y 軸旋轉的數量

### <a name="microsoftperceptionsimulationisimulatedhand"></a>Microsoft.PerceptionSimulation.ISimulatedHand

描述模擬人類看得交介面

```
public interface ISimulatedHand
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    bool Activated { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    bool Visible { [return: MarshalAs(UnmanagedType.Bool)] get; }
    void EnsureVisible();
    void Move(Vector3 translation);
    void PerformGesture(SimulatedGesture gesture);
}
```

**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**

擷取與世界相關節點的位置，以公尺為單位

**Microsoft.PerceptionSimulation.ISimulatedHand.Position**

擷取和設定相對於人類，模擬的左手邊的位置以公尺為單位。

**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**

會擷取和設定是否手形目前已啟動。

**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**

擷取目前可看見 （亦即，它是 HandTracker 可以偵測到的位置） SimulatedDevice 手形是否。

**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**

它會顯示以 SimulatedDevice，請移動手形。

**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**

移動模擬的左手邊的位置，相對於其目前的位置，以公尺為單位。

參數
* 轉譯-要轉移模擬的手的數量

**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**

執行使用 （它只會偵測到系統如果啟用了 hand） 模擬的手動動作。

參數
* 筆勢-要執行的筆勢

### <a name="microsoftperceptionsimulationisimulatedhead"></a>Microsoft.PerceptionSimulation.ISimulatedHead

描述模擬人類的標頭的介面

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**

擷取與世界相關節點的位置，以公尺為單位

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**

擷取模擬的標頭的旋轉。 正數時尋找沿著軸順時針旋轉弧度為單位。

**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**

擷取模擬標頭的直徑。 此值用以判斷前端的中心 （旋轉的點）。

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**

旋轉模擬的標頭，相對於其目前的旋轉角度。 正數時尋找沿著軸順時針旋轉弧度為單位。

參數
* 輪替-要旋轉的數量

### <a name="microsoftperceptionsimulationisimulationrecording"></a>Microsoft.PerceptionSimulation.ISimulationRecording

播放，載入與單一的錄製內容互動的介面。

```
public interface ISimulationRecording
{
    StreamDataTypes DataTypes { get; }
    PlaybackState State { get; }
    void Play();
    void Pause();
    void Seek(UInt64 ticks);
    void Stop();
};
```

**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**

擷取錄製中的資料類型的清單。

**Microsoft.PerceptionSimulation.ISimulationRecording.State**

擷取記錄的目前狀態。

**Microsoft.PerceptionSimulation.ISimulationRecording.Play**

開始播放。 如果記錄已暫停，播放會繼續從暫停的位置;如果停止，將會開頭開始播放。 如果已播放，則會忽略這個呼叫。

**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**

暫停播放其目前的位置。 如果停止錄製時，會忽略呼叫。

**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**

（在從一開始的 100 奈秒間隔） 會設法在指定的時間錄製與暫停在該位置。 如果記錄結尾以外的位置時，它會暫停在最後一個畫面格。

參數
* 刻度-要搜尋的時間

**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**

停止播放，並且重設到開頭的位置

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a>Microsoft.PerceptionSimulation.ISimulationRecordingCallback

在播放期間接收的狀態變更的介面

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**

當 ISimulationRecording 播放狀態變更時呼叫

參數
* newState-錄製的新狀態

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.PerceptionSimulationManager

建立 Perception 模擬物件的根物件

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**

產生模擬的封包，並將其傳遞至所提供的接收的物件上建立。

參數
* 接收-將會收到所有產生的封包的接收

傳回值

建立的管理員

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**

建立儲存在指定路徑的檔案中的所有接收的封包的接收。

參數
* path-建立檔案的路徑

傳回值

建立的接收

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**

從指定的檔案載入記錄

參數
* 路徑-要載入之檔案的路徑
* 處理站-錄製用於建立 ISimulationStreamSink 時所需的處理站

傳回值

載入的記錄

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording (System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory，Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**

從指定的檔案載入記錄

參數
* 路徑-要載入之檔案的路徑
* 處理站-錄製用於建立 ISimulationStreamSink 時所需的處理站
* 回呼的回呼會接收更新 regrading 錄製的狀態

傳回值

載入的記錄

### <a name="microsoftperceptionsimulationstreamdatatypes"></a>Microsoft.PerceptionSimulation.StreamDataTypes

說明不同類型的資料流資料

```
public enum StreamDataTypes
{
    None = 0x00,
    Head = 0x01,
    Hands = 0x02,
    SpatialMapping = 0x08,
    Calibration = 0x10,
    Environment = 0x20,
    All = None | Head | Hands | SpatialMapping | Calibration | Environment
}
```

**Microsoft.PerceptionSimulation.StreamDataTypes.None**

用來表示任何資料流的資料類型之 sentinel 值

**Microsoft.PerceptionSimulation.StreamDataTypes.Head**

Stream 的位置和方向的標頭的相關資料

**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**

Stream 的位置和指針的筆勢的相關資料

**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**

Stream 的空間的對應環境的相關資料

**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**

Stream 的校正裝置的相關資料。 在遠端模式系統只接受校正封包。

**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**

Stream 的 關於裝置的環境資料

**Microsoft.PerceptionSimulation.StreamDataTypes.All**

用來表示所有記錄的資料類型之 sentinel 值

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a>Microsoft.PerceptionSimulation.ISimulationStreamSink

接收資料封包從模擬的資料流物件

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**

接收單一封包時，也就是在內部具類型和版本設定

參數
* length-將封包的長度
* 封包-封包的資料

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a>Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory

物件，可建立 ISimulationStreamSink

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**

建立 ISimulationStreamSink 的單一執行個體

傳回值

建立的接收