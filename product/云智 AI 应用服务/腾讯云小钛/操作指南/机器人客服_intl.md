## Knowledge Base
Knowledge base is used to locate customer questions. Bot will automatically answer customers if matching knowledge points exist in the knowledge base. Otherwise, it won't be able to answer. Bot can keep supplementing knowledge base by question learning so that customer intents can be accurately identified.
Knowledge base consists of professional Q&As, chitchat, synonyms and industry-specific knowledge base.

### Professional Q&As
You can view standard Q&As in **Knowledge Base Management** > **Knowledge Base** > **Professional Q&As**.
Professional Q&As is the most important part of knowledge base as it effectively improves the bot’s question answering capability. Professional Q&As are logged as question and answer pairs.

Using the knowledge base:
1. Select a knowledge category
2. Add a question
3. Add similar questions
4. Review the knowledge base
5. Test Q&As
6. Knowledge Maintenance

#### 1. Select a knowledge category
Selecting a knowledge category to better query and manage  knowledge rules. You can view professional Q&As in a certain category. The categories can be added, edited, sorted and deleted.
![](https://main.qcloudimg.com/raw/4b0d6df340a81c61c6e6ba15c02dff69.png)

#### 2. Add a standard question
In **Knowledge Base Management** > **Knowledge Base** > **Professional Q&As**, click **Add a question** to enter standard questions, similar questions and standard answers. An answer can be text, hyperlink or image.
Basic principles for question formatting:
- Similar questions should not be too short.
- There must be subjects and predicates.
- Intent must be complete. An answer can be given based on the question without any further probing.
 Correct question examples: What should I do if I lost my train ticket? How to upload an image? How long does it take to deliver the product?
 Incorrect question examples: train station, image, delivery
 Example of knowledge to be entered:
 Standard question: Where is Wuhan Railway Station?
 Similar question: Where is Wuchang Railway Station located? / How to get to Wuchang Railway Station? / How can I get to Wuchang Railway Station? /······
 Answer: Wuchang Railway Station is located at 642 Zhongshan Road, Wuchang District, Wuhan.

**New knowledge points are by default enabled and permanently valid. You can disable or set validity periods based on your needs. Batch configuration is also supported.**

#### 3. Add similar questions
Similar questions can be added to increase the match rate. The more similar questions, the higher the match rate. It is generally required to add 5 or more similar questions.
You can add similar questions in two ways:
- When adding a standard question, add a similar question in the similar question input box on the next line (up to 150 questions can be added).
- Add all similar questions after adding standard questions.
  If no similar questions has been added, you can export the existing knowledge points from the knowledge base and then add similar questions for the knowledge points in batches.

#### 4. Add associated questions
Associated questions are questions that are relevant to a given question, such as a different concern for the same matter. When a customer asks a question, the system will list associated questions while giving the answer.
![](https://main.qcloudimg.com/raw/9412a2e0cd1c1758658a5b5c85eed6c0.png)
After adding a standard question, click **Add an associated question** in the lower left corner of the answer input box to add an associated question.
You can turn on/off the automatic recommendation of associated questions (off by default) in **System Management** > **Bot Settings** > **Associated Questions**.

#### 5. Batch add
When using the bot for the first time, it is recommended that you enter the FAQs in the form of Q&A pair into the Excel template we provide for batch import into the knowledge base. The batch addition steps are as follows:
1. In **Knowledge Base Management** > **Knowledge Base**, click **Batch Import** and download the "Professional Q&As Template" in the popup.
2. Enter standard questions, categories, answers, similar questions and associated questions into the appropriate cells in the Excel file.
3. After completing the template, click **Batch Import** in **Knowledge Base Management** > **Knowledge Base** to upload the completed file.
4. After uploading, you can check the quantities of successfully uploaded/failed questions. If the upload fails, please check whether the file format and size are correct and whether the number of entries is within the limit, correct if necessary and then retry.

#### 6. Review the knowledge base
You can review the entered knowledge in **Knowledge Base Management** > **Knowledge Base** > **Pending tasks** > **Professional Q&As** > **To be reviewed**.
- The knowledge entered by an admin does not need to be reviewed and can be included directly into the knowledge base.
- The knowledge entered by an agent needs to be reviewed by an admin and will be included into the knowledge base after approval (if it is rejected, it can be re-submitted after the question/answer is modified).

#### 7. Knowledge Maintenance
During actual use, you need to constantly modify and improve the knowledge base:
- Delete duplicate and obsoleted knowledge on a regular basis.
- Adjust the way of composing questions appropriately based on real customer questions.
- Add more similar questions to better understand customer intents and improve the efficiency and match rate of knowledge points.
- Intelligently learn similar questions and unknown questions.

### Chitchat conversations

#### Add chitchat Q&As

Chitchat refers to conversations that have nothing to do with the professional Q&As, such as "The weather is really good". Chitchat is enabled by default in the system, and a common chitchat corpus is configured (i.e., the default chitchat conversations). In addition to the default chitchat corpus, you can also configure a personal chitchat corpus where text, images and hyperlinks can be added as answers.
You can add, edit and delete chitchat conversations in **Knowledge Base Management** > **Knowledge base** > **Chitchat conversations**. Example of chitchat conversation:
![](https://main.qcloudimg.com/raw/91583c7aca96d27cbb5b86e10c8726be.png)

#### Notes
- In admin mode:
 - When adding a chitchat question, if no answer is added, you can click **OK** directly to add the question to **Knowledge Base Management** > **Pending tasks** > **Chitchat conversations** > **To be edited**, where you can enter the answer to the question. After that, the question will be transferred to **Knowledge Base Management** > **Knowledge base** > **Chitchat conversations** in admin mode and take effect;
 - Add a complete pair of standard Q&A and click **OK** to add it to **Chitchat conversations** in admin mode which will take effect directly.
- In agent mode:
 - When adding a chitchat question, if no answer is added, you can click **OK** directly to add the question to **Knowledge Base Management** > **Pending tasks** > **Chitchat conversations*, where you can enter the answer to the question. After that, the question will be transferred to **Knowledge Base Management** > **Knowledge base** > **Chitchat conversations** > **To be reviewed** in admin mode and wait for review by an admin;
 - Add a complete pair of standard Q&A and click **OK** to add it to **To be reviewed** in admin mode which will be reviewed by an admin.

#### Add chitchats in batches
Click **Batch import**, download the Excel spreadsheet titled "Chitchat Conversations Template" and enter the chitchat Q&As in the required format into the template.
![img](https://iask.qq.com/static/docs/images/data_chat_4.png) After the chitchat conversations template is completed, click "Select a file" or drag and drop the template to the specified area to upload it.
- After the upload is successful, you can see the file name, the prompt for "Upload succeeded", the quantities of successfully uploaded/failed questions as well as the locations and reasons for failures for troubleshooting.
- If the upload fails, please check whether the file format and size are correct and whether the number of entries is within the limit, correct if necessary and then retry.

#### Export chitchat Q&As
Click **Export to Excel** in the upper right corner and click **Download** to export all the chitchat Q&A pairs in the knowledge base into an Excel spreadsheet.

### Synonyms

#### Add synonyms
Synonyms are two words with similar meanings. After synonyms are added and configured, the bot will semantically understand the synonyms and match them with questions. For example, "cell phone" and "mobile phone" are synonyms.
In **Knowledge Base Management** > **Knowledge base**, select the **Synonyms** tab to add synonyms for standard words one by one or in batches.
- **Add one by one** 
  Click **Add a synonym** and enter the standard word and its synonyms (up to 20 synonyms can be added for one standard word).
- **Batch add** 
  Click **Batch import**, download the synonym template as prompted, complete and then upload it.

#### Notes
- In admin mode:
 - When adding a standard word, if no synonym is added, you can click **OK** directly to add the word to **Knowledge Base Management** > **Pending tasks** > **Synonyms** > **To be edited**, where you can enter the synonyms. After that, the synonyms will be transferred to **Knowledge Base Management** > **Knowledge base** > **Synonyms** in admin mode and take effect.
 - Add a standard word and its synonyms and click **OK** to add them to **Knowledge Base Management** > **Knowledge base** > **Synonyms** in admin mode which will take effect directly.
- In agent mode:
  - When adding a standard word, if no synonym is added, you can click **OK** directly to add the word to **Knowledge Base Management** > **Pending tasks** > **Synonyms**, where you can enter the synonyms. After that, the synonyms will be transferred to **Knowledge Base Management** > **Pending tasks** > **Synonyms** > **To be reviewed** in admin mode and wait for review by an admin.
  - Add a standard word and its synonyms and click **OK** to add them to **Knowledge Base Management** > **Pending tasks** > **Synonyms** > **To be reviewed** in admin mode which will be reviewed by an admin.

### Industry-specific knowledge base
TICSR comes with generic knowledge base of 10 industries including e-commerce and education, helping you jump start right from the first access. If your organization built good knowledge base already, the knowledge base can be added to the professional Q&A directly.
1. In **Knowledge Base Management** > **Knowledge base**, select the **Industry-specific knowledge base** tab.
2. Click **Import** for your industry to import your industry-specific knowledge base.

>! Industry-specific knowledge base will be effective imediately after importing. Be careful if you import another industry's knowledge base. Enter the professional Q&As and delete the knowledge base if you made a mistake.

## Testing Q&As

You can start a test conversation with the bot in **Knowledge Base Management** > **Q&As test**. If no answer is found for a question, you can optimize the relevant knowledge point according to the matching results. **The system will retain the test results of the past 3 days. You can add test questions directly to the knowledge base if needed.**
You can optimize the knowledge base according to the different types of matches in the test results.

**Match type:**
- Exact match: The bot directly matches the customer questions with standard or similar questions in the knowledge base.
- Fuzzy match: If the customer question is not clear enough, the bot will probe.
- Bottom match: The bot replies with a bottom answer to a customer question that cannot be understood.
- Chitchat: The bot recognizes the question as a chitchat conversation.



## Pending Tasks
- Incomplete Q&A pairs and synonym pairs in the knowledge base will be transferred to the **Pending tasks** > **To be edited** list.
- Complete Q&A pairs and synonym pairs added to the knowledge base by an agent will be transferred to the **Pending tasks** > **To be reviewed** list.
  ![img](https://iask.qq.com/static/docs/images/task_1.png)

### Admin mode
#### Tasks to be edited
- Edit: Click **Edit** on the right to add or modify an answer or synonym in the edit window. After the operation is completed, the question will be transferred to the knowledge base and take effect.
- Delete: Delete a Q&A pair or synonym pair.
- Transfer: Select to transfer a question to a specific agent. After the transfer, the question will be transferred to **Knowledge Base Management** > **Pending tasks** in agent mode.

### Agent mode
#### Edit a pending task
Click **Edit** on the right to add or modify an answer or synonym in the edit window. After the operation is completed, the Q&A pair or synonym will be transferred to **Knowledge Base Management** > **Pending tasks** > **Chitchat conversations** > **To be reviewed** in admin mode and wait for review by an admin.

## Smart Learning
To better understand customer intention, improve efficiency and knowledge match rate, it is necessary to have smart learning for bots, duplicate and obsoleted knowledge deletion on a regular basis, question modification based on real customer inputs and similar questions adding.

### Smart training
You can make customer service bots smarter and more accurate in answering questions by training them.
Intelligent training is divided into knowledge base conditions and learning conditions:
- **Knowledge base conditions**: The system will calculate the average similarity of current questions in the knowledge base. The higher the average similarity, the smarter the bot. Click "Supplement" to add a similar question to trigger bot training.
- **Learning conditions**: This refers to the learning based on current similar questions, unknown questions and dissatisfaction analysis. Click "Supplement" to edit the corresponding module.

#### Training the bot
You can train bots by clicking "Train the bot" in smart learning.
There are six stages in bot training: rudimentary, beginner, intermediate, enhanced, advanced and mature. Their numbers of similar questions are 5, 10, 20, 30, 40, and 50 respectively. You need to meet similar question numbers and have no pending content to go trigger training.
There will be one training after meeting corresponding bot training condition. There will be no training if there is no newly added content.

### Learn similar questions
Similar questions are questions that are of high quality and can be associated with standard questions. It is recommended to select "Approve" or "Associate a similar question" for them. If there is a mistake, select "Ignore". This can improve the ability of machine learning.
![img](https://iask.qq.com/static/docs/images/study_2.png)
### Learn unknown questions
Unknown questions are questions to which no answers can be found in the knowledge base. It is recommended to add them as new questions to supplement the knowledge base and improve the ability of machine learning.
![img](https://iask.qq.com/static/docs/images/study_3.png)

### Learn unsatisfactory questions
If the customer rates an answer as unsatisfactory, the question and the corresponding answer will appear in the unsatisfactory question learning tab, and it is recommended to correct the unsatisfactory answer.
![img](https://iask.qq.com/static/docs/images/study_4.png)
- **Approve**: Add the question as a similar question for a standard question matched by the algorithm.
- **Associate with another question**: Add the question as a similar question for a standard question already in the knowledge base.
- **Add as a new question**: Add the question as a new standard question.
- **Ignore**: Delete the question learning record.
- **Correct the answer**: Go to the edit page of the knowledge point and modify the answer or question.

## Bot Settings
In **System Management** > **Bot settings**, you can set basic bot information, chitchat function, bot conversation reply template and trending questions. **This can be used only by admins.**

### Basic settings
Different greetings and templates for unknown and alternative questions can be set for different platforms (WeChat Official Account, WeChat Mini Program, desktop websites and mobile website). Rich text answers can be added to conversations. **In bot mode, customer inquiries only supports text but not other formats.**

**Greeting (unavailable for the WeChat Official Account channel)**: When the customers opens the conversation window, they will receive the greeting message from the bot before sending the first message.
**Reply to unknown questions**: This is the reply sent by the system when the bot cannot recognize the customer's intent or match an answer or similar questions.
![img](https://iask.qq.com/static/docs/images/setting_base_2.png)
**Replies to alternative questions**: This is to probe the customer. When the customer question is not clear or the bot cannot fully recognize the customer's intent, the system will return a list of probing questions (1-5 questions can be configured).
![img](https://iask.qq.com/static/docs/images/setting_base_3.png)

### Trending questions
Trending questions are the questions most frequently asked by customers. This is an important function, and proper configuration of it can greatly improve the answer efficiency of the bot. Trending questions are supported for desktop websites, mobile websites, WeChat Mini Programs WeChat Official Accounts.
- When the customer accesses the service via a desktop or mobile website, the system will actively push the trending questions to the customer after greeting. If the customer questions is meaningless or unclear and cannot be recognized, the system may also trigger trending questions to guide the customer to select an appropriate question or probe the customer, which can improve the efficiency of communication between the customer and the bot.
- When the customer accesses the service via a WeChat Official Account, trending questions will be triggered only if the customer questions is meaningless or unclear and cannot be recognized.
- When the customer accesses the service via a WeChat Mini Program, the greeting and trending questions will be actively pushed to the customer.
>? When the customer accesses the service via a WeChat Official Account for the first time or if the customer hasn't asked the bot in over 48 hours, the trending questions cannot be actively pushed.
You can enable this function in **System Management** > **Bot settings** > **Trending questions**. This function is disabled by default. If you want to use it, please turn it on manually.

- Configure the prompt for trending questions
  ![](https://main.qcloudimg.com/raw/7198aaf684b1364985213e409fcb6381.png)
- Trending questions configuration: Level 2 trending questions are supported and can be added to the categories (from the knowledge base).
  ![](https://main.qcloudimg.com/raw/4a9673c0caf2a759f91ff193ff04dca3.png)
If a level 1 question has been configured, an answer can be sent directly; if a level 2 question has been configured, it will be sent upon the first inquiry. The prompt for and display of level 1 trending questions are as shown below:
![img](https://iask.qq.com/static/docs/images/setting_hot_6.png)
The prompt for and display of level 2 trending questions are as shown below:
![img](https://iask.qq.com/static/docs/images/setting_hot_7.png)

### Associated questions
You can enable associated questions in **System Management** > **Bot settings** > **Associated questions**. This function is disabled by default. If you want to use it, please turn it on manually.
Associated questions are questions that are relevant to a given question, such as a different concern for the same matter. You can add questions or configure them during batch import in **Knowledge base** > **Standard Q&As**.

Associated questions can be associated manually or automatically:
**Manually associated questions** can be configured in **Knowledge base** > **Add a question**/**Batch import questions**. After associated questions are manually configured for question A, when a customer asks question A, the bot will list the associated questions while giving the answer.
**Automatically associated questions** are automatically recommended by the algorithm with no manual configuration required when a knowledge graph is present. At present, knowledge graphs and automatic recommendations by algorithm are available only for **project-based products**. If associated questions have been configured in the knowledge base, they will be recommended preferably.
The display effect is as follows:
![](https://main.qcloudimg.com/raw/6d25514fef241e34d03794d49452082e.png)

### Satisfaction rating

You can enable satisfaction rating in **System management** > **Bot settings** > **Satisfaction rating**. This function is disabled by default. If you want to use it, please turn it on manually.
After this function is enabled, the customer can rate the answers by the bot, and the statistical results can be viewed in the operational data. This function can be turned on by channel and a rating description style can be set.
The satisfaction rating button will appear only when an answer appears (if it is a level 1 or level 2 question, the button won't be displayed).
![img](https://iask.qq.com/static/docs/images/setting_review_2.png)
