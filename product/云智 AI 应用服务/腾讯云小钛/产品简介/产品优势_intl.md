## Knowledge Graph-based Conversations
Traditional Q&A database is unable to interpret incomplete expressions or handle excessive inquiries. Tencent Big Data AI team utilized field-specific knowledge graphs in creating operation models, and on that foundation, they built the multi-round conversation system. The system uses natural language understanding technology to identify parts of customer intentions before searching through the knowledge graph network to customers for further elaboration. The system also has context memory.

## Learning Model and Cold Start Solution Based on Deep Migration Learning
TICSR integrates traditional machine learning and deep learning models. Traditional machine learning model captures character matched information while deep learning model captures question semantic correlations. The two combined strengthens the system’s stability no matter the size of the data volumes.

Traditional customer service systems is based on question matching, has few similar questions, and is unable to train a stable model. TICSR's deep migration learning, however, uses general corpus (not provided by users) to train the basic model, and adopts user-provided smaller corpus for migration learning. An integrated model is generated to train stable models even if the cold start Q&A database there is unsophisticated. Offline evaluation tests have proven that for 1 similar question, the accuracy of the deep migration learning model is 40% higher than that of the traditional model, and when there are 5 similar questions, accuracy improves by 100%.

## Corpus Mining Based on Big Data
Based on Tencent's big data warehouse, we can find customer questions from certain fields' corpus that are industry-related. These questions can be used to train deep learning models and create Q&A database. The data solution is a unique asset to Tencent's Big Data team, helping users efficiently build Q&A database in cold starts.
