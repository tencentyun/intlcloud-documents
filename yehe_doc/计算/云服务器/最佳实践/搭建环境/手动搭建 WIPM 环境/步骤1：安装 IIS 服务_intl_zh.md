## 操作场景

本文档以 Windows Server 2012 R2 操作系统和 Windows Server 2008 操作系统为例，介绍在 Windows 云服务器上进行 IIS 角色添加与安装。

## 操作步骤
### Windows Server 2012 R2 操作系统
1. 登录 Windows 云服务器。
2. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img>，打开服务器管理器。如下图所示：
![](https://main.qcloudimg.com/raw/cae0fe0bfebf5ad58b6e5d3451795230.png)
3. 单击【添加角色和功能】，弹出 “添加角色和功能向导” 窗口。
4. 在 “添加角色和功能向导” 窗口中，单击【下一步】。
5. 在 “选择安装类型” 界面，选择【基于角色或基于功能的安装】，并连续单击2次【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/9eaff4f125fb23a7180cba6f38f9f879.png)
6. 在 “选择服务器角色” 界面，勾选【Web 服务器(IIS)】。如下图所示：
弹出 “添加 Web 服务器(IIS) 所需的功能” 提示框。
![](https://main.qcloudimg.com/raw/d0aa5fa075275bfb2bd0c68da66616e4.png)
7. 在弹出的 “添加 Web 服务器(IIS) 所需的功能” 提示框中，单击【添加功能】。如下图所示：
![](https://main.qcloudimg.com/raw/817d1f22107836c77af2fd963888824f.png)
8. 单击【下一步】。
9. 在 “选择功能” 界面，勾选【.NET Framework 3.5 功能】，并连续单击2次【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/4876efa4308912eb4bdbb6074d35fd20.png)
10. 在 “选择角色服务” 界面，勾选【CGI】，单击【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/c571820b1a4290d9b04abbc65cf81fd9.png)
11. 确认安装信息，单击【安装】，并等待安装完成。如下图所示：
![](https://main.qcloudimg.com/raw/1e51aed773aad8eac28f88c401a1814e.png)
12. 安装完成后，在云服务器的浏览器中访问 `http://localhost/`，验证 IIS 是否安装成功。
若出现以下界面，即表示成功安装。
![](https://mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

### Windows Server 2008 操作系统

1. 登录 Windows 云服务器。
2. 在操作系统界面，单击 <img src="https://main.qcloudimg.com/raw/0e33f3dc1042244ab225ca32c5396296.png" style="margin: 0;"></img>，打开服务器管理界面。如下图所示：
![](https://main.qcloudimg.com/raw/36c9cf3d9fd246f0930a4be3516446b5.png)
3. 在左侧导航栏中，选择【角色】，并在右侧窗口中单击【添加角色】。如下图所示：
![](https://main.qcloudimg.com/raw/b18a3c84aa193d3c64d1e25353154baf.png)
4. 在打开的 “添加角色向导” 窗口中，单击【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/4ab72f46730ecf10f2fe2768b2cc24cc.png)
5. 在 “选择服务器角色” 界面，勾选【Web 服务器 (IIS)】，并连续单击2次【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/7a41185e562a62ca586b6b677381b3a1.png)
6. 在 “选择角色服务” 界面，勾选【CGI】，单击【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/7e7a96b106292e87d44807369db66842.png)
7. 确认安装信息，单击【安装】，并等待安装完成。如下图所示：
![](https://main.qcloudimg.com/raw/877b71930f11d9d2a6fecf946f0bebfe.png)
8. 安装完成后，在云服务器的浏览器中访问 `http://localhost/`，验证 IIS 是否安装成功。
若出现以下界面，即表示成功安装。
![](https://main.qcloudimg.com/raw/b11cd8170e7646daa3b9ca904b181cf4.png)

