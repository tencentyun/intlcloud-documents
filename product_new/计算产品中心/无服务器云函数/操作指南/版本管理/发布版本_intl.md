## Operation Scenario

After configuring the function, submitting the code, and passing the online test, you can fix the version of the function by releasing the version to avoid errors or execution failures of online business caused by subsequent modification and testing of the code. You can release a version at any time, and in all releases, the $LATEST version is always the latest version.

## Steps

>? A function has the $LATEST version attribute upon its creation. The $LATEST version points to the currently editable version and is always present and editable. 

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf).
2. In the navigation pane on the left, select "Functions" to enter the service information page. See the figure below:
![](https://main.qcloudimg.com/raw/33b3b7982dd3ff66f206da2ac66c3b8a.png)
3. Select the region of the function, choose the desired function from the list and enter the function information page.
4. Click **Release a new version** at the top right of the function information page. See the figure below:
![](https://main.qcloudimg.com/raw/cec2a5607438c15bf9961c4dfd569a94.png)
5. In the "Reminder" window that pops up, enter the release description and click **Submit** to release the function.
>!
> - When the release is submitted, the SCF platform will generate a copy of the configuration and code content of the current $LATEST version of the function and save it as version content.
> - After the release is completed, the version number of the current release will be generated. The version number starts from 1 and increments for each release with no upper limit.
> - The released version only records and fixes the configuration and code of the current $LATEST version of the function, but not the trigger configuration of the function. The newly released function does not have any triggers.
