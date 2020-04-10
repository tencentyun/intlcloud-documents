## Feature Overview
Web application firewalls on the market mainly use two detection methods, one based on regex rules and the other on semantics rules. As the methods have inherent limitations, "false positives" and "false negatives" cannot be completely avoided. To solve this problem, Tencent Cloud WAF leverages machine learning-based web attack detection technology. With the self-learning, self-evolvement, and adaptation capabilities of the AI engine, it can maximize the detection success rate and capture rate for known and unknown threats, minimize false positives, and flexibly adapt to ever-changing web applications.
## Configuration Case 
1. **Set the AI engine mode**
	1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia) and select **Web Application Firewall** > **Protection Settings** on the left sidebar. In the domain name list, click the domain name to be protected to enter the protection settings page, and click **Basic Settings** to set the AI engine mode to **Observe**.
 
	2. On the left sidebar, select **Web Application Firewall** > **Attack Details** to enter the attack log page and click **Log Query**. On the pop-up page, you can view logs of attacks detected by the AI engine. This attack type is recorded as "Detected by AI Engine". You can use filters to view attack logs of this type.

2. **Perform online AI verification**
On the left sidebar, select **Web Application Firewall** > **AI Engine** to enter the AI engine page and click **Online AI Verification**. On the pop-up page, you can verify the `GET`, `POST`, and `HEADER` parameters of the specified access address. When a correct parameter is mistakenly identified by the AI engine as incorrect, you can click **Add False Positive** to add this false positive to the false positive list. The following uses parameter `a` with a value of `1 and 1=1` as an example to describe how to do so.

3. **Process a false positive in the AI engine**
Click the **AI False Positive Processing** tab to view the added false positive records. You can also manually add a false positive to the list. In the status column, click **Learn** and the AI engine will update the model and optimize the algorithm based on the false positive information.

> When the AI engine learns the payload of a submitted false positive, it will take a certain period of time to change from unlearned to learned status. Please wait patiently.
>
After the AI engine completes learning the payload of the submitted false positive, you can check whether this parameter will trigger false positives again on the **Online AI Verification** page.

4. **Add a false negative**
When the payload of an attack is missed by the AI engine (false negative), you can click **Add False Negative** to add the false negative information to the false negative list. The following uses parameter `a` with a value of `admin^*$` as an example to describe how to do so.

5. **Process the false negative in the AI engine**
 Click the **AI False Negative Processing** tab to view the added false negative records. You can also manually add a false negative to the list. In the status column, click **Learn** and the AI engine will update the model and optimize the algorithm based on the false negative information.

>When the AI engine learns the payload of a submitted false negative, it will take a certain period of time to change from unlearned to learned status.
>
After the AI engine completes learning the payload of the submitted false negative, you can check whether this parameter will trigger false negatives again on the **Online AI Verification** page.

## Notes
- The AI engine uses a strict mode with the highest protection level.
- The AI engine can learn from the feedback you manually provide in the console and also supports self-learning on the backend.
- You are recommended to enable the "Observe" mode of the AI engine for a certain period of time (such as 20 days). If you directly enable the "Block" mode, false positives may occur at a low probability.
- The AI engine and the rule engine are in series. When malicious requests are blocked by the rule engine, they will not be sent to the AI engine for detection; when they are allowed by the rule engine, they will be sent to and blocked by the AI engine.
- False positive submission methods:
 1. On the **AI False Positive Processing** page, manually add a false positive.
 2. On the **Online AI Verification** page, confirm that a verified payload is a false positive and submit it.
 3. On the left sidebar, select **Web Application Firewall** > **Attack Details**, click a log entry whose attack type is "Detected by AI Engine", confirm that this attack is a false positive, and add it to the list.
     
     >For false positive attacks of the same type, you only need to add one of them as a false positive.
- False negative submission methods:
 1. On the **AI False Negative Processing** page, manually add a false negative.
 2. On the **Online AI Verification** page, confirm that a verified payload is a false negative and submit it.
- If a submitted false positive or negative is found incorrect later, you can select it on the **AI False Positive Processing** or **AI False Negative Processing** page and click **Delete** to delete it.
