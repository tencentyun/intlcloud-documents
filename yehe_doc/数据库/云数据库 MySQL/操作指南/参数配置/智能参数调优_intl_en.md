This document describes how to implement intelligent parameter tuning in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).

## Background
The concept of "deep learning" has been gaining popularity among general users. As relevant technologies are getting more mature, the TencentDB team is thinking about how to use deep learning to improve the operating efficiency of databases. The first thing that comes to mind is database parameter tuning. Due to the huge differences in business systems, it is impossible to perform targeted tuning in a fine-grained manner like optimizing SQL, which is a challenge for DBAs. They often have to draw upon their experience to build a set of better performing parameter templates. The ability to tune database parameters is more like an exclusive skill of expert DBAs.

Between 2019 and 2021, the TencentDB team published two papers entitled "Automatic Database Tuning Using Deep Reinforcement Learning" and "An Online Cloud Database Hybrid Tuning System for Personalized Requirements" respectively, and applied for international patents for the theory. Now, the theory is developed into a usable system based on the papers, which improves the database performance by tuning parameters in real-world use cases.

**Why database parameter tuning?**
- **High numbers of parameters**: For example, MySQL has hundreds of configuration items, so tuning is difficult.
- **High labor costs**: A full-time DBA is required, and expert experience is needed, which incur high labor costs.
- **Poor tool universality**: Existing tools have limited features and involve time-consuming operations, producing a poor effect.
- **New requirements in the cloud**: Some users don't have a full-time Ops team, making it impossible to implement parameter tuning.

## Prerequisites
You have a running TencentDB for MySQL instance.

## Use Limits
- Scenario-based intelligent tuning can be performed only three times per instance per month. This limit is reset on the first day of each month.
- AI-based intelligent analysis (coming soon) can be performed only once per instance per month. This limit is reset on the first day of each month.
- Intelligent parameter tuning can be performed only for instances with at least four CPU cores.
- The intelligent parameter tuning task list keeps only the last 15 tuning results.
- When an instance is terminated/returned or expires, any ongoing intelligent parameter tuning task in it will be automatically aborted and deleted.
- Only one tuning task can be executed per instance at any time.
- The intelligent parameter tuning feature currently is supported only in Beijing, Shanghai, and Guangzhou regions and will be available in more regions in the future.

## Directions
### Previously purchased MySQL instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and select a region at the top. In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management** > **Parameter Settings** > **Intelligent Parameter Tuning**.
![](https://qcloudimg.tencent-cloud.cn/raw/a1231071d9542857295c3875d25038a3.png)
3. In the **Intelligent Parameter Tuning** pop-up window, select **Scenario-Based Intelligent Tuning** or **AI-Based Intelligent Analysis** as the tuning method and click **Analyze**.
![](https://qcloudimg.tencent-cloud.cn/raw/88a18f17f80772ea67a0c7127fd74218.png)
 - If you select **Scenario-Based Intelligent Tuning**, follow the steps below:
**Scenario-based intelligent tuning**: An efficient and targeted intelligent analysis based on your selected scenario.
 Select a business scenario in the **Scenario** drop-down list, which can be **Order Transactions**, **OLTP Performance Test**, or **Pressure Test**.
 After selecting a scenario, you can customize the business ratio in the scenario for more accurate system analysis. Then, click **Analyze**.
    - Order Transactions (TPCC)
      - Customizable items: Order processing (high), Payment (high), Order query (low), Logistics (low), Warehousing (low)
      - Data Reading Mode: Cache (default), Disk + Cache
      - Concurrency: Low, Middle, High (default)
    - OLTP Performance Test (Sysbench)
      - Customizable items: Reading data (high), Writing data (none by default)
      - Data Reading Mode: Cache (default), Disk + Cache
      - Concurrency: Low, Middle, High (default)
    - Pressure Test (myslap)
      - Concurrency: Low, Middle, High (default)
![](https://qcloudimg.tencent-cloud.cn/raw/6e8dac90a50b17e84199b3f6776a2d90.png)
 - If you select **AI-Based Intelligent Analysis** (coming soon), follow the steps below:
**AI-Based Intelligent Analysis**: The database business type is determined through in-depth analysis of database operating metrics, the performance of different parameters in specific scenarios is analyzed with deep learning algorithms, and then parameter suggestions are presented.
After selecting **AI-Based Intelligent Analysis**, click **Analyze**.
>!
>- The AI-based intelligent analysis is under improvement and will be available soon.
>- This is a time-consuming intelligent analysis based on deep learning algorithm and big data analytics. We recommend you perform it during off-peak hours.
4. The parameter tuning task starts when the analysis starts. You can select **Intelligent Parameter Tuning** > **View Task** on the **Parameter Settings** page to view the task details.
![](https://qcloudimg.tencent-cloud.cn/raw/1c66551fd214b1775bf33bdd4a98a935.png)
5. After the parameter tuning task is completed, you can click **View Results** in the **Operation** column in **Intelligent Parameter Tuning** > **View Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/895d52add70eb601b4e5c994f634cbfc.png)
6. After confirming the parameter tuning recommendations, click **Apply to Instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/39a40c1a3cc2a26bef76ccdbee0f129e.png)
7. Confirm the parameter change in the pop-up window, select the **Execution Mode**, read and indicate your consent to the **Restart Rules**, and click **OK**.
Execution mode:
  - Immediate execution: The change will be applied to the instance immediately after the confirmation.
  - During maintenance time: The change will be applied to the instance during the maintenance time, which can be modified on the **Instance Details** page.

### Newly purchased MySQL instance
When purchasing a TencentDB for MySQL instance, after selecting a parameter template, you can choose whether to enable **Scenario-Based Intelligent Tuning**. If this feature is enabled, the system will perform secondary adjustment according to the selected business scenario, which can be **Order Transactions**, **OLTP Performance Test**, or **Pressure Test**.
You can view the change results in **Parameter Settings** > **Intelligent Parameter Tuning** > **View Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/bf0e00d4ba24814e1bad20f17cd50575.png)

