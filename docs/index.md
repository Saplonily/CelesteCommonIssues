# Celeste 常见问题及 Q 群指令集

## 蔚蓝本体报错

### 如何找到并发送 log.txt?
`/log.txt`  
首先打开游戏根目录, 如果是 steam 平台你还可以通过右键游戏, 展开 `管理`, 点击 `浏览游戏文件` 来打开, 然后在对应目录下寻找或搜索 `log.txt`.  
注意不要发送此文件打开后的截图, 请发送完整的文件.

### Ionic.Zip.ZipException: Could not read xxx as a zip file
`/badzip`  
```log
Ionic.Zip.ZipException: Could not read D:\SteamLibrary\steamapps\common\Celeste\Mods\StrawberryJam2021AudioA.zip as a zip file
 ---> Ionic.Zip.ZipException: Cannot read that as a ZipFile
 ---> Ionic.Zip.BadReadException:   Bad signature (0x00000000) at position  0x10BD5A53
   at Ionic.Zip.ZipEntry.ReadHeader(ZipEntry ze, Encoding defaultEncoding)
   at Ionic.Zip.ZipEntry.ReadEntry(ZipContainer zc, Boolean first)
   at Ionic.Zip.ZipFile.ReadIntoInstance_Orig(ZipFile zf)
   at Ionic.Zip.ZipFile.ReadIntoInstance(ZipFile zf)
   --- End of inner exception stack trace ---
```
某一个 mod 的压缩包损坏了, 尝试删除 xxx 对应的 mod 并重新下载.  
如果你曾使用过 cele-mod 那么这大概率是 cele-mod 的一个 bug 造成的.

### System.DllNotFoundException: 无法加载 xxx: 找不到指定的模块。
`/missingdll`  
```log
2024/4/14 14:40:18
System.DllNotFoundException: 无法加载 DLL“CSteamworks”: 找不到指定的模块。 (异常来自 HRESULT:0x8007007E)。
   在 Steamworks.NativeMethods.SteamAPI_RestartAppIfNecessary(AppId_t unOwnAppID)
   在 Celeste.Celeste.Main(String[] args)
```
如果 xxx 为 `CSteamworks`, 你需要验证游戏完整性(`/verifyfiles`), 然后重装 Everest.  
如果 xxx 为 `lua54.dll`, 重复上一条的步骤, 如果问题依然没有被解决, 你可以尝试一个临时解决方案:  
在游戏根目录找到名为 `lib64-` 开头的文件夹, 然后将其中的 `lua54.dll` 文件复制到游戏根目录. (例如在 x64 Windows 平台上文件夹名为 `lib64-win-x64`)

### System.Exception: FMOD Failed: xxx
`/fmodissue`  
```log
Ver 1.4.0.0-fna [Everest: 4465-azure-52f83]
03/30/2024 22:49:39
System.Exception: FMOD Failed: ERR_OUTPUT_INIT (Error initializing output device.)
   at Celeste.Audio.CheckFmod(RESULT result) in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Audio.cs:line 42
   at Celeste.Audio.Update()
   at Celeste.Celeste.Update(GameTime gameTime)
   at Microsoft.Xna.Framework.Game.Tick() in /tmp/FNA/src/Game.cs:line 430
   at Microsoft.Xna.Framework.Game.RunLoop() in /tmp/FNA/src/Game.cs:line 875
   at Microsoft.Xna.Framework.Game.Run() in /tmp/FNA/src/Game.cs:line 416
   at Monocle.Engine.RunWithLogging() in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Monocle/Engine.cs:line 52
```
如果 xxx 为 `ERR_OUTPUT_INIT` 或者 `ERR_NOTREADY`, 那这是 fmod 日常抽风了, 请插拔你的音频设备或者重启电脑.
如果 xxx 为 `ERR_EVENT_ALREADY_LOADED`, 这是你安装的 mod 之间有重复的音频或者你重复安装了同一个 mod, 请尝试关闭一些 mod 或关闭重复的 mod, 必要时你可以向发生冲突 mod 的作者反馈这个问题.

### System.OutOfMemoryException: 没有足够的内存继续执行程序。 (xna)
`/fna`  
```log
Ver 1.4.0.0
2024/4/5 13:32:00
System.OutOfMemoryException: 没有足够的内存继续执行程序。
   在 Microsoft.Xna.Framework.Helpers.GetExceptionFromResult(UInt32 result)
   在 Microsoft.Xna.Framework.Graphics.GraphicsHelpers.GetExceptionFromResult(UInt32 result)
   在 Microsoft.Xna.Framework.Graphics.GraphicsDevice.Present(tagRECT* pSource, tagRECT* pDest, HWND__* hOverride)
   在 Microsoft.Xna.Framework.GraphicsDeviceManager.Microsoft.Xna.Framework.IGraphicsDeviceManager.EndDraw()
   在 Microsoft.Xna.Framework.Game.EndDraw()
   在 Microsoft.Xna.Framework.Game.DrawFrame()
   在 Microsoft.Xna.Framework.Game.Tick()
   在 Microsoft.Xna.Framework.Game.HostIdle(Object sender, EventArgs e)
   在 Microsoft.Xna.Framework.GameHost.OnIdle()
   在 Microsoft.Xna.Framework.WindowsGameHost.RunOneFrame()
   在 Microsoft.Xna.Framework.WindowsGameHost.ApplicationIdle(Object sender, EventArgs e)
   在 System.Windows.Forms.Application.ThreadContext.System.Windows.Forms.UnsafeNativeMethods.IMsoComponent.FDoIdle(Int32 grfidlef)
   在 System.Windows.Forms.Application.ComponentManager.System.Windows.Forms.UnsafeNativeMethods.IMsoComponentManager.FPushMessageLoop(IntPtr dwComponentID, Int32 reason, Int32 pvLoopData)
   在 System.Windows.Forms.Application.ThreadContext.RunMessageLoopInner(Int32 reason, ApplicationContext context)
   在 System.Windows.Forms.Application.ThreadContext.RunMessageLoop(Int32 reason, ApplicationContext context)
   在 System.Windows.Forms.Application.Run(Form mainForm)
   在 Microsoft.Xna.Framework.WindowsGameHost.Run()
   在 Microsoft.Xna.Framework.Game.RunGame(Boolean useBlockingRun)
   在 Monocle.Engine.RunWithLogging()
```
这是 steam 默认版本所使用的一个过时底层框架在 win11 上的一个 bug.
在 steam 中右键游戏, 选择 `属性`, 然后打开 `测试版`, 在 `参与测试` 选择 `opengl - opengl` 并更新你的游戏.

### System.InvalidProgramException: Common Language Runtime detected an invalid program.
`/invalidprogram`  
```log
System.InvalidProgramException: Common Language Runtime detected an invalid program.
   at System.Runtime.CompilerServices.RuntimeHelpers.CompileMethod(RuntimeMethodHandleInternal method)
   at invoke RuntimeHelpers.CompileMethod(RuntimeMethodHandle )
   at MonoMod.Core.Platforms.Runtimes.FxCoreBaseRuntime.GetMethodHandle(MethodBase method)
   at MonoMod.Core.Platforms.Runtimes.FxCoreBaseRuntime.Compile(MethodBase method)
   at MonoMod.Core.Platforms.PlatformTriple.Compile(MethodBase method)
   at MonoMod.Core.Platforms.PlatformTripleDetourFactory.Detour.CreateDetour()
...
```
某些 helper 之间出现了偶然的冲突, 请更新你所有的 mod, 如果仍然出现此问题尝试关闭一些 mod.

### System.InvalidOperationException: Present failed! Error Code: GPU
```log
...
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code:  (0x8007000E)
Texture2D creation failed! Error Code: GPU ?��?????????????? GetDeviceRemovedReason (0x887A0005)
Present failed! Error Code: GPU ?��?????????????? GetDeviceRemovedReason (0x887A0005)
(01/06/2024 20:08:28) [Everest] [Error] [crit-error-handler] >>>>>>>>>>>>>>> ENCOUNTERED A CRITICAL ERROR <<<<<<<<<<<<<<<
--------------------------------
System.InvalidOperationException: Present failed! Error Code: GPU ?��?????????????? GetDeviceRemovedReason (0x887A0005)
   at Microsoft.Xna.Framework.FNALoggerEXT.FNA3DLogError(IntPtr msg) in /tmp/FNA/src/FNALoggerEXT.cs:line 98
   at Microsoft.Xna.Framework.Graphics.FNA3D.FNA3D_SwapBuffers(IntPtr device, IntPtr sourceRectangle, IntPtr destinationRectangle, IntPtr overrideWindowHandle)
   at Microsoft.Xna.Framework.Graphics.GraphicsDevice.Present() in /tmp/FNA/src/Graphics/GraphicsDevice.cs:line 554
   at Microsoft.Xna.Framework.Game.Tick() in /tmp/FNA/src/Game.cs:line 430
   at Microsoft.Xna.Framework.Game.RunLoop() in /tmp/FNA/src/Game.cs:line 875
   at Microsoft.Xna.Framework.Game.Run() in /tmp/FNA/src/Game.cs:line 416
   at Monocle.Engine.RunWithLogging() in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Monocle/Engine.cs:line 52
```

暂时未知原因, 尝试关闭一些 mod.  
如果 `log.txt` 中还出现了大量下述字样:
```log
Image loading failed: outofmem
Image loading failed: no SOI
```
这是一个底层框架的 bug, 不过解决方案依然是尝试关闭一些 mod.

### System.NullReferenceException: Object reference not set to an instance of an object.
如果后面紧跟的是这一串:
```log
System.NullReferenceException: Object reference not set to an instance of an object.
   at Celeste.Mod.CelesteNet.Client.CelesteNetClientModule.Load()
   at Celeste.Mod.Everest.Register(EverestModule module)
   at Celeste.Mod.Everest.Loader.LoadModAssembly(EverestModuleMetadata meta, Assembly asm)
   at Celeste.Mod.Everest.Loader.LoadMod(EverestModuleMetadata meta)
   at Celeste.Mod.Everest.CheckDependenciesOfDelayedMods()
   at Celeste.Mod.Everest.Register(EverestModule module)
   at Celeste.Mod.Everest.Loader.LoadMod(EverestModuleMetadata meta)
   at Celeste.Mod.Everest.Loader.LoadModDelayed(EverestModuleMetadata meta, Action callback)
   at Celeste.Mod.Everest.Loader.LoadZip(String archive)
   at Celeste.Mod.Everest.Loader.LoadAuto()
   at Celeste.Mod.Everest.Boot()
   at Celeste.Celeste..ctor()
```
`/miaonet317crash`  
这是群服在旧版 Everest 上的 bug, 更新你的 Everest 到最新的 stable.

### Yo, I heard you like Everest so I put Everest in your Everest so you can Ever Rest while you Ever Rest.
别看 `errorlog.txt` 了, 快去看 `log.txt`.

### System.ArgumentNullException: Value cannot be null. (Parameter 'collection')
`/updatemiaonet`  
```log
System.ArgumentNullException: Value cannot be null. (Parameter 'collection')
   at System.Collections.Generic.List`1.InsertRange(Int32 index, IEnumerable`1 collection)
   at Celeste.Mod.Everest.get_InstallationHash() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.cs:line 195
   at DMD<System.Void Celeste.AreaComplete:InitAreaCompleteInfoForEverest2(System.Boolean, Celeste.Session)>(Boolean pieScreen, Session session)
   at Celeste.Mod.Randomizer.RandoModule.EverestDontIntrospect(Action`2 orig, Boolean pieScreen, Session session)
   at Hook<Celeste.AreaComplete::InitAreaCompleteInfoForEverest2>?25158407(Boolean , Session )
   at Hook<System.Void TAS.EverestInterop.AreaCompleteInfo::AreaCompleteOnInitAreaCompleteInfoForEverest2(On.Celeste.AreaComplete+orig_InitAreaCompleteInfoForEverest2,System.Boolean,Celeste.Session)>(Boolean , Session )
   at SyncProxy<System.Void Celeste.AreaComplete:InitAreaCompleteInfoForEverest2(System.Boolean, Celeste.Session)>(Boolean , Session )
   at Celeste.AreaComplete.Begin()
...
```
更新你的群服, 也就是 `Miao.CelesteNet.Client`, 这是群服在新版 Everest 上的 bug.

### System.InvalidOperationException: Present failed! Error Code:  (0x887A0020)
```log
System.InvalidOperationException: Present failed! Error Code:  (0x887A0020)
   at Microsoft.Xna.Framework.FNALoggerEXT.FNA3DLogError(IntPtr msg) in /tmp/FNA/src/FNALoggerEXT.cs:line 98
   at Microsoft.Xna.Framework.Graphics.FNA3D.FNA3D_SwapBuffers(IntPtr device, IntPtr sourceRectangle, IntPtr destinationRectangle, IntPtr overrideWindowHandle)
   at Microsoft.Xna.Framework.Graphics.GraphicsDevice.Present() in /tmp/FNA/src/Graphics/GraphicsDevice.cs:line 554
   at Microsoft.Xna.Framework.Game.Tick() in /tmp/FNA/src/Game.cs:line 430
   at Microsoft.Xna.Framework.Game.RunLoop() in /tmp/FNA/src/Game.cs:line 875
   at Microsoft.Xna.Framework.Game.Run() in /tmp/FNA/src/Game.cs:line 416
   at Monocle.Engine.RunWithLogging() in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Monocle/Engine.cs:line 52
```
目前已知该报错仅会在显卡 `Intel(R) Iris(R) Xe Graphics` 上发生, 这是一个显卡内部驱动问题.  
目前可以通过更改渲染 api 解决:
打开游戏根目录下的 `everest-launch.txt` 后将 `# --graphics opengl` 一行去除前面的 `#`, 也就是变为 `--graphics opengl`, 然后保存该文件.

### Ionic.Zlib.ZlibException: Bad state (invalid block type)
`/badzip-nofilename`  
```log
Ionic.Zlib.ZlibException: Bad state (invalid block type)
   at Ionic.Zlib.InflateManager.Inflate(FlushType flush)
   at Ionic.Zlib.ZlibBaseStream.Read(Byte[] buffer, Int32 offset, Int32 count)
   at Ionic.Crc.CrcCalculatorStream.Read(Byte[] buffer, Int32 offset, Int32 count)
   at System.IO.Stream.CopyTo(Stream destination, Int32 bufferSize)
   at Celeste.Mod.ModAsset.WriteCache(String path) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/ModAsset.cs:line 182
   at Celeste.Mod.ModAsset.GetCachedPath() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/ModAsset.cs:line 148
   at Celeste.Audio.IngestBank(ModAsset asset) in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Audio.cs:line 170
   at DMD<System.Void Celeste.Audio:Init()>()
   at Celeste.Mod.SpeedrunTool.Other.MuteInBackground.AudioOnInit(orig_Init orig)
   at Hook<System.Void Celeste.Mod.SpeedrunTool.Other.MuteInBackground::AudioOnInit(On.Celeste.Audio+orig_Init)>()
   at SyncProxy<System.Void Celeste.Audio:Init()>()
   at DMD<System.Void Celeste.GameLoader:LoadThread()>(GameLoader this)
   at Hook<System.Void Celeste.Mod.SkinModHelper.LoaderHook::GameLoaderLoadThreadHook(On.Celeste.GameLoader+orig_LoadThread,Celeste.GameLoader)>(GameLoader )
   at SyncProxy<System.Void Celeste.GameLoader:LoadThread()>(GameLoader )
   at Celeste.RunThread.RunThreadWithLogging(Action method)
```
某个 mod 的压缩包损坏了, 但是报错没有说明具体是哪个文件, 尝试只开一半的 mod 并使用二分法查找具体是哪个 mod 的压缩包损坏了.

### System.IO.IOException: 磁盘空间不足。 : 'C:\Users\Administrator\AppData\Local\Temp\tmp837F.tmp'
```log
System.IO.IOException: 磁盘空间不足。 : 'C:\Users\Administrator\AppData\Local\Temp\tmp837F.tmp'
   at System.IO.RandomAccess.WriteAtOffset(SafeFileHandle handle, ReadOnlySpan`1 buffer, Int64 fileOffset)
   at System.IO.Strategies.OSFileStreamStrategy.Write(ReadOnlySpan`1 buffer)
   at System.IO.Strategies.OSFileStreamStrategy.Write(Byte[] buffer, Int32 offset, Int32 count)
   at System.IO.Strategies.BufferedFileStreamStrategy.WriteSpan(ReadOnlySpan`1 source, ArraySegment`1 arraySegment)
   at System.IO.Strategies.BufferedFileStreamStrategy.Write(Byte[] buffer, Int32 offset, Int32 count)
   at Celeste.Mod.Everest.Relinker.GetRelinkedAssembly(EverestModuleMetadata meta, String asmname, Stream stream, Stream symStream, MissingDependencyResolver depResolver, String[] checksumsExtra, Action`1 prePatch) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Relinker.cs:line 153
   at Celeste.Mod.EverestModuleAssemblyContext.LoadAssemblyFromModPath(String path, String asmName) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Module/EverestModuleAssemblyContext.cs:line 185
   at Celeste.Mod.Everest.Loader.LoadMod(EverestModuleMetadata meta) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 494
   at Celeste.Mod.Everest.Loader.LoadModDelayed(EverestModuleMetadata meta, Action callback) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 457
   at Celeste.Mod.Everest.Loader.LoadZip(String archive) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 320
   at Celeste.Mod.Everest.Loader.LoadAuto() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 185
   at Celeste.Mod.Everest.Boot() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.cs:line 461
   at Celeste.Celeste..ctor() in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Celeste.cs:line 274
```
检查你的磁盘是否真的满了.

### System.IO.FileNotFoundException: Could not load file or assembly 'System.Runtime, Version=7.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies. 系统找不到指定的文件。
`/7.0runtime`  
```log
System.IO.FileNotFoundException: Could not load file or assembly 'System.Runtime, Version=7.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies. 系统找不到指定的文件。
   at System.ModuleHandle.ResolveType(RuntimeModule module, Int32 typeToken, IntPtr* typeInstArgs, Int32 typeInstCount, IntPtr* methodInstArgs, Int32 methodInstCount, ObjectHandleOnStack type)
   at System.ModuleHandle.ResolveTypeHandleInternal(RuntimeModule module, Int32 typeToken, RuntimeTypeHandle[] typeInstantiationContext, RuntimeTypeHandle[] methodInstantiationContext)
   at System.RuntimeType.RuntimeTypeCache.MemberInfoCache`1.PopulateNestedClasses(Filter filter)
   at System.RuntimeType.RuntimeTypeCache.MemberInfoCache`1.GetListByName(Char* pName, Int32 cNameLen, Byte* pUtf8Name, Int32 cUtf8Name, MemberListType listType, CacheType cacheType)
   at System.RuntimeType.RuntimeTypeCache.MemberInfoCache`1.Populate(String name, MemberListType listType, CacheType cacheType)
   at System.RuntimeType.RuntimeTypeCache.MemberInfoCache`1.GetMemberList(MemberListType listType, String name, CacheType cacheType)
   at System.RuntimeType.GetNestedTypeCandidates(String fullname, BindingFlags bindingAttr, Boolean allowPrefixLookup)
   at System.RuntimeType.GetNestedTypes(BindingFlags bindingAttr)
   at Celeste.Mod.Everest.LuaLoader.CachedType._Crawl() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.LuaLoader.Caches.cs:line 73
   at Celeste.Mod.Everest.LuaLoader.CachedType..ctor(Type type) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.LuaLoader.Caches.cs:line 51
   at Celeste.Mod.Everest.LuaLoader.Precache(Assembly asm) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.LuaLoader.cs:line 152
   at Celeste.Mod.Everest.Register(EverestModule module) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.cs:line 584
   at Celeste.Mod.Everest.Loader.LoadModAssembly(EverestModuleMetadata meta, Assembly asm) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 0
   at Celeste.Mod.Everest.Loader.LoadMod(EverestModuleMetadata meta) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 0
   at Celeste.Mod.Everest.Loader.LoadModDelayed(EverestModuleMetadata meta, Action callback) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 0
   at Celeste.Mod.Everest.Loader.LoadZip(String archive) in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 0
   at Celeste.Mod.Everest.Loader.LoadAuto() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.Loader.cs:line 104
   at Celeste.Mod.Everest.Boot() in /home/vsts/work/1/s/Celeste.Mod.mm/Mod/Everest/Everest.cs:line 326
   at Celeste.Celeste..ctor() in /home/vsts/work/1/s/Celeste.Mod.mm/Patches/Celeste.cs:line 236
```

某些 mod 依赖了最新的 Everest 但是没有在依赖中写明, 更新 Everest 到 4465 及以上的版本.

### System.Exception: Can't find sprite xxx
`/skinmodissue`  
```log
System.Exception: Can't find sprite CollabUtils2/miniHeart/bgr/ with index 0
   at Monocle.Sprite.GetFrames(String path, Int32[] frames)
   at Monocle.Sprite.AddLoop(String id, String path, Single delay, Int32[] frames)
   at DMD<System.Void Monocle.SpriteData:Add(System.Xml.XmlElement, System.String)>(SpriteData this, XmlElement xml, String overridePath)
   at Hook<System.Void Celeste.Mod.CelesteNet.Client.CelesteNetClientSpriteDB::OnSpriteDataAdd(On.Monocle.SpriteData+orig_Add,Monocle.SpriteData,System.Xml.XmlElement,System.String)>(SpriteData , XmlElement , String )
   at SyncProxy<System.Void Monocle.SpriteData:Add(System.Xml.XmlElement, System.String)>(SpriteData , XmlElement , String )
   at Monocle.SpriteBank.orig_ctor(Atlas atlas, XmlDocument xml)
   at Celeste.Mod.CollabUtils2.CollabModule.reloadCrystalHeartSwapSpriteBanks()
   at Celeste.Celeste.LoadContent()
   at Microsoft.Xna.Framework.Game.Initialize()
   at Monocle.Engine.Initialize()
   at Celeste.Celeste.orig_Initialize()
   at Celeste.Celeste.Initialize()
   at Microsoft.Xna.Framework.Game.DoInitialize()
   at Microsoft.Xna.Framework.Game.Run()
   at Monocle.Engine.RunWithLogging()
```
这是 SkinModHelper 与 SkinModHelperPlus 的一个 bug, 也就是皮肤 mod 的前置. 尝试更新这两个 mod. 如果问题依然出现只能暂时关闭这俩 mod.

### System.OutOfMemoryException: Insufficient memory to continue the execution of the program.
```log
System.OutOfMemoryException: Insufficient memory to continue the execution of the program.
   at System.Runtime.InteropServices.Marshal.AllocHGlobal(IntPtr cb)
   at DMD<System.Void Monocle.VirtualTexture:Reload()>(VirtualTexture this)
   at Celeste.Mod.CollabUtils2.LazyLoadingHandler.onTextureLazyLoad(orig_Reload orig, VirtualTexture self)
   at Hook<System.Void Celeste.Mod.CollabUtils2.LazyLoadingHandler::onTextureLazyLoad(On.Monocle.VirtualTexture+orig_Reload,Monocle.VirtualTexture)>(VirtualTexture )
   at SyncProxy<System.Void Monocle.VirtualTexture:Reload()>(VirtualTexture )
   at Monocle.VirtualTexture.<>c__DisplayClass50_0.<Reload>b__1()
```
原因未知, 可能是某个底层库的问题, 尝试关闭一些 mod.

### Steam not found!
`/steamnotfound`  
尝试重启你的 steam, 问题依然出现的话尝试重启你的电脑. 如果同时还是非正版用户的话, 这是因为 Everest 4465+ 版本改动了 steam 验证相关的内容, 具体解决方案相信以你的经验是能解决这个问题的.

### System.IO.FileNotFoundException: Could not load file or assembly 'CelesteNet.Client, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies.
`Guneline` mod 与群服出现的兼容问题, 如果该 mod 是必要的那只能暂时关闭群服 mod (注意不仅仅是关闭与群服的连接).

## Everest 安装报错

### 如何找到 miniinstaller-log.txt?
`/installer-log`  
首先打开游戏根目录, 如果是 steam 平台你还可以通过右键游戏, 展开 `管理`, 点击 `浏览游戏文件` 来打开, 然后在对应目录下寻找或搜索 `miniinstaller-log.txt`.  
注意不要发送此文件打开后的截图, 请发送完整的文件.

### System.IO.IOException: 文件 xxx 正由另一进程使用，因此该进程无法访问此文件。
`/savefileinuse`  
```log
File not found, skipping: osx\libtheorafile.dylib
File not found, skipping: osx\libvulkan.1.dylib
Saves\0.celeste -> orig\Saves\0.celeste
Failed installing 4722 (stable)
System.IO.IOException: 文件“H:\SteamLibrary\steamapps\common\Celeste\orig\Saves\0.celeste”正由另一进程使用，因此该进程无法访问此文件。
   在 System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
   在 System.IO.File.InternalCopy(String sourceFileName, String destFileName, Boolean overwrite, Boolean checkHost)
   在 MonoMod.Installer.GameModder._Backup()
   在 MonoMod.Installer.GameModder.Install()
Error! Please check installer-log.txt
```

如果 xxx 文件以 `.celeste` 结尾, 也就是存档文件的话, 请删除蔚蓝根目录下的 `orig` 文件夹并重试.

### System.BadImageFormatException: Format of the executable (.exe) or library (.dll) is invalid.
`/badpefile`  
```log
System.BadImageFormatException: Format of the executable (.exe) or library (.dll) is invalid.
   at Mono.Cecil.PE.ImageReader.ReadOptionalHeaders(UInt16& subsystem, UInt16& dll_characteristics)
   at Mono.Cecil.PE.ImageReader.ReadImage()
   at Mono.Cecil.PE.ImageReader.ReadImage(Disposable`1 stream, String file_name)
   at Mono.Cecil.ModuleDefinition.ReadModule(Disposable`1 stream, String fileName, ReaderParameters parameters)
   at Mono.Cecil.ModuleDefinition.ReadModule(String fileName, ReaderParameters parameters)
   at MonoMod.MonoModder._ReadModule(String input, ReaderParameters args) in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/MonoModder.cs:line 359
   at MonoMod.MonoModder.MapDependency(ModuleDefinition main, String name, String fullName, AssemblyNameReference depRef) in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/MonoModder.cs:line 503
   at MonoMod.MonoModder.MapDependency(ModuleDefinition main, AssemblyNameReference depRef) in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/MonoModder.cs:line 400
   at MonoMod.MonoModder.MapDependencies(ModuleDefinition main) in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/MonoModder.cs:line 397
   at MonoMod.MonoModder.MapDependencies() in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/MonoModder.cs:line 388
   at MonoMod.Program.Main(String[] args) in /home/vsts/work/1/s/external/MonoMod/src/MonoMod.Patcher/Program.cs:line 72
```
游戏文件损坏了, 验证游戏文件完整性后重试. (`/verifyfiles`)

### System.TypeInitializationException: The type initializer for 'MonoMod.InlineRT.MonoModRulesManager' threw an exception.
`/old-eveinstaller`  
```log
MonoMod 22.1.4.3
System.TypeInitializationException: The type initializer for 'MonoMod.InlineRT.MonoModRulesManager' threw an exception. ---> System.IO.FileNotFoundException: Could not load file or assembly 'System.Collections, Version=7.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies. 系统找不到指定的文件。
   at MonoMod.InlineRT.MonoModRulesManager..cctor()
   --- End of inner exception stack trace ---
   at MonoMod.InlineRT.MonoModRulesManager.Register(MonoModder self)
   at MonoMod.MonoModder..ctor()
   at MonoMod.Program.Main(String[] args)
```

使用的 `Everest.Installer` 版本太旧了, 更新到最新版本后重试.

## Loenn 报错

### utils/filesystem.lua:40: invalid value (nil) at index 1 in table for 'concat'
`/loenn-cnchar`  
```log
Editor version: 0.7.10
Love2d version: 11.4.0 - Mysterious Mysteries
Operating system: Windows

utils/filesystem.lua:40: invalid value (nil) at index 1 in table for 'concat'


Traceback

[love "callbacks.lua"]:228: in function 'handler'
[C]: in function 'concat'
utils/filesystem.lua:40: in function 'joinpath'
celeste_render.lua:24: in function 'f'
selene/selene/wrappers/searcher/love2d/searcher.lua:16: in function <selene/selene/wrappers/searcher/love2d/searcher.lua:13>
[C]: in function 'require'
loaded_state.lua:4: in function 'f'
selene/selene/wrappers/searcher/love2d/searcher.lua:16: in function <selene/selene/wrappers/searcher/love2d/searcher.lua:13>
[C]: in function 'require'
tool_utils.lua:1: in function 'f'
...
[C]: in function 'require'
scenes/loading.lua:40: in function 'firstEnter'
scene_handler.lua:126: in function 'changeScene'
scenes/startup.lua:34: in function 'saveGotoLoading'
scenes/startup.lua:114: in function <scenes/startup.lua:109>
scene_handler.lua:46: in function 'update'
selene_main.lua:38: in function 'update'
main.lua:61: in function <main.lua:25>
[C]: in function 'xpcall'
```

你的用户名包含了中文字符, 临时的解决方案需要为 Loenn 的 exe 文件新建一个快捷方式, 然后右键打开其属性, 在 `快捷方式` 栏的 `目标` 后面添加 ` --portable` (注意空格和双横杠),
例如 `"D:\Softwares\Loenn\Lönn.exe"` 更改为 `"D:\Softwares\Loenn\Lönn.exe" --portable`, 然后使用该快捷方式打开 Loenn.

## 其他指令

### `/verifyfiles`
在 steam 上: 右键游戏, 选择 `属性`, 打开 `已安装文件` 页面, 点击 `验证游戏文件的完整性`, 然后 steam 会开始下载缺失和不匹配的文件.  
注意此操作会清除你的 Everest 安装, 你需要重新安装 Everest.

### `/zip`
在打包你的 mod 时不要对着文件夹右键点击压缩, 你需要进入文件夹内, 全选文件(Ctrl + A), 然后再右键选择压缩. 压缩等级推荐选最低等级, 压缩等级过高可能会轻微拖慢游戏启动速度.

### `/hardlist`
hist 榜链接:
[https://docs.google.com/spreadsheets/d/1A88F3X2lOQJry-Da2NpnAr-w5WDrkjDtg7Wt0kLCiz8/edit#gid=1904725075](https://docs.google.com/spreadsheets/d/1A88F3X2lOQJry-Da2NpnAr-w5WDrkjDtg7Wt0kLCiz8/edit#gid=1904725075)

### `/goldenlist`
金榜链接:
[https://docs.google.com/spreadsheets/u/1/d/1v0yhceinMGr5alNekOxEkYCxXcYUsbtzMRVMezxbcVY/edit](https://docs.google.com/spreadsheets/u/1/d/1v0yhceinMGr5alNekOxEkYCxXcYUsbtzMRVMezxbcVY/edit)