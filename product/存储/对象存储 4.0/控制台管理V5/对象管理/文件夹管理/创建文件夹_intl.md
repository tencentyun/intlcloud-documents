In COS that comes with no folders, objects are stored in a flat structure. To make it easier for you to get started, objects named by using "/" as suffix in the object key can be used as "folders". In fact, the storage space of a "folder" in COS is 0.
> <font color="#0000cc">**Note:**</font>
The folder name is limited to 255 characters, and [Reserved Characters and Fields](#保留字符和字段) are not supported.

## Naming Rules for Folders
1. A combination of numbers, letters and visible characters is supported.
2. A folder cannot begin with `/` and does not allow two or more consecutive `/`.
3. A subdirectory can be created quickly by separating the path by `/`.
4. The folder name cannot be empty.
5. Do not use `..` as the folder name.

<span id="Reserved Characters and Fields"></span>
## Reserved Characters and Fields
- Reserved characters: [con], [aux], [nul], [prn], [com0], [com1], [com2], [com3], [com4], [com5], [com6], [com7], [com8], [com9], [lpt0], [lpt1], [lpt2], [lpt3], [lpt4], [lpt5], [lpt6], [lpt7], [lpt8], and [lpt9].
- Reserved ASCII control characters:
Up (↑): CAN (24)
Down (↓): EM (25) 
Right (→): SUB (26) 
Left (←): ESC (27) 

## Steps
1. Log in to the [COS console](https://intl.cloud.tencent.com/login), and select **Bucket List** from the left side bar to enter the Bucket List page. Click the bucket you want to create folder and enter the bucket.
![](https://main.qcloudimg.com/raw/8675c78498b1d65599a95945174bc567.png)
2. Click **Create folder** and the **Create new folder** dialog box pops up.
![](https://main.qcloudimg.com/raw/0d7592f9fa0dba6e59d408d09cf44303.png)
3. Enter the folder name and click **OK** to save it.
![](https://main.qcloudimg.com/raw/867050320892e102b928a8ac925794f2.png)

