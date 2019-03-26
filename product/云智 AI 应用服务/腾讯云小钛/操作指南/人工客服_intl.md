## Enabling Human Customer Service
You can enable human customer service in **System Management** > **Human customer service settings** > **Human customer service**.
After human customer service is enabled, if a bot fails to give an answer or the customer explicitly asks for human assistance, an agent will be accessed.
- **Conversation channel settings**: You can set the access channels and conditions for human customer service by selecting and editing variables.
- **Human customer service hours settings**: You can set the human customer service hours (accurate down to the minute) by selecting and editing the configuration item.
- **Queuing settings**: You can edit the prompts for queuing and keywords for proactive leaving.

## Agent Workbench

The entry to the agent workbench is the button located at the bottom right of the page. All ongoing conversations and frequently used actions and options are available in this panel.
The workbench is divided into three zones from left to right, i.e., conversation list, conversation messages and extended functions.
![](https://main.qcloudimg.com/raw/13376ca50a9d01dea12ded2c0e2f4738.jpg)
**Conversation list zone:**
The conversation list contains **name of the current agent**, **status**, **number of customers in the queue**, **number of customers automatically transferred to the current agent** and **customer in the current conversation**.

**Status**: There are two types of login status for agents and admins: online and paused.
- Online: When an agent logs in to the customer service system in the normal way, their status is "online". When the agent is online, new conversations can be automatically transferred to them.
- Paused: When the agent becomes overwhelmed with the workload, they can proactively switch the status to "paused". If the agent is paused, new conversations will not be automatically transferred to them, but ongoing conversations can continue to be processed.

**Automatically transferable number**: This number can be set in **People Management** > **Account management**. When the current number of attended customers is greater than or equal to the number of automatically transferable customers, the system will no longer automatically assign conversations to the agent.

**Conversation messages zone:**
This zone displays the historical messages between the agent and customers and the message input box for the agent. The functions of the five icons in the conversation messages zone are as detailed below:
1. Screenshot function (for Windows only).
2. Intelligent assistance: The bot will recommend an answer in the lower right corner to each customer question. If the agent considers the bot's recommendation appropriate, they can directly click the answer and send it to the customer.
3. Transfer: This transfers the customer to another online agent, who can view the conversation record of the previous agent.
4. Send an image.
5. Collect a question: This collects a valuable Q&A in the conversation into the knowledge base (only one answer can be collected for one question).

**Extended functions zone:**
In this zone, the agent can view customer information and use quick answer tools. The quick answer corpus can be set in **Agent workbench** > **Quick answer corpus**.

## Message Board

You can enable the message board in **System Management** > **Human customer service settings** > **Message board settings**. This function is disabled by default. If you want to use it, please turn it on manually. Currently, it is supported only for the mobile version and desktop website version.
In non-working hours such as holidays or if no agents are online, customers will not be able to get customer service. In this case, you can enable the message board and provide an alternative channel for customer feedback.

### Configure the message board
You can configure the message board header text, prompt text for question description, contact information options and image upload options in **System Management** > **Human customer service settings** > **Message board settings**.
![](https://main.qcloudimg.com/raw/bf54747762c5b211c513e3fe057b3e37.png)
Entry to the message board page:
![](https://main.qcloudimg.com/raw/407030117f8592bbadef71b80281d4cf.png)

### View a message
An agent can view customer messages in **Agent workbench** > **Message board** and contact a customer by the contact information (phone or email) provided by the customer.
![](https://main.qcloudimg.com/raw/a25f7fe200f783af4bf871636dbc0155.png)
- Open: After a customer leaves a message successfully, the message can be viewed in the Open tab.
- Closed: This tab lists customer messages that have been processed by an agent.

## Conversation Record
You can view the history of bot conversations and agent conversations and batch export conversation statistics in **Agent workbench** > **Conversation record**.
![img](https://iask.qq.com/static/docs/images/rengongkefu17.png)
If a customer is successfully transferred to an agent during the conversation with a bot, the conversation will be counted as an agent conversation but not bot conversation.

## Quick Answer Corpus
The quick answer corpus is a set of scripts frequently used by agents when answering customer questions. It is divided into two parts: public corpus and personal corpus.
- The public corpus is edited and managed by an admin, and agents can use but not edit it. The admin can set up multiple level 1 categories for public quick answers.
- The personal corpus is edited and managed by an agent or admin. The agent can set up multiple level 1 categories for personal quick answers.

You can add a quick answer by clicking **Add** in **Agent workbench** > **Quick answer corpus** and entering the keywords and answer content.

## Satisfaction Rating
You can enable satisfaction rating in **System management** > **Human customer service settings** > **Satisfaction rating**. This function is disabled by default. If you want to use it, please turn it on manually.
The satisfaction rating button will appear only after the customer leaves the conversation.
![](https://main.qcloudimg.com/raw/e45d200fdaf598d2eb1de90abc0fba31.png)
Below is an example:
![img](https://iask.qq.com/static/docs/images/rengongkefu6.png)

## Conversation Settings
In **System Management** > **Conversation settings**, you can set the **Conversation ending by customer** and **Sensitive words**.
- **Conversation ending by customer**: You can configure the words indicting the customer's intent to end the conversation with agent and the end button for HTML5 and desktop websites.
- **Sensitive words**: If the conversation contains the configured sensitive words, the words will be replaced with asterisks (*) in the messages.
  ![](https://main.qcloudimg.com/raw/eb8775ea906f24fb1a47c364c50d82ea.png)
