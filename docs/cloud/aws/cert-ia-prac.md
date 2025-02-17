# AWS Certified IA Practitioner

## Security
- Use IAM to implement role-based access controls to restrict data access to authorized personnel only.
- Use cryptographic hashing techniques to verify the authenticity of the data.

## Characteristics of a Generative AI
- Personalization is a critical capability for generative AI. It involves tailoring content or recommendations to individual users based on their preferences or characteristics, which enhances user experiences and engagement.
- Scalability can handle increasing workloads efficiently. It's crucial for large-scale applications.
- Data efficiency relates to how well a model can learn from limited data.
- Simplicity is essential for user adoption and system maintenance, it only indirectly impacts personalized recommendations. The real complexity lies in understanding user preferences, not in the simplicity of the AI model itself.
- Adaptability ensures versatility across different scenarios.
- Responsiveness matters for chatbots and virtual assistants, real-time responsiveness.

## Challenges of Generative AI
- Toxicity refers to the risk of generating content that is offensive, disturbing, or inappropriate. This challenge is compounded by the subjective nature of defining what constitutes toxic content, which can vary based on context and culture. Furthermore, detecting and mitigating subtle or indirect offensive language adds to the complexity of managing toxicity in generative AI outputs.
- Hallucinations are assertions or claims made by generative AI models that sound plausible but are factually incorrect. Due to the nature of LLMs, which generate text based on patterns rather than factual verification, they may produce convincing yet erroneous information. For instance, LLMs can generate fictitious scientific citations or non-existent references that appear legitimate but are inaccurate.
- Intellectual Property concerns arise when generative AI models produce content that mimics or reproduces elements of their training data. This can lead to legal issues if the generated content closely resembles copyrighted material or reproduces it verbatim. For example, an AI-generated image in the style of a famous artist could raise objections if it closely mimics the artist's original work.
- Disruption of the Nature of Work refers to how generative AI can change job roles or automate tasks rather than issues of ownership and attribution.
- Plagiarism and Cheating
- Knowledge cutoff: Generative AI models are trained on datasets available up to a certain point in time, and they do not have access to real-time data or updates. This limitation can result in the models providing outdated information, which is especially problematic in dynamic environments where up-to-date knowledge is crucial. The knowledge cutoff can limit the effectiveness of the AI in providing accurate and relevant responses to customers.

## Generative AI models
- Large language models (LLMs) are extensive deep learning models pre-trained on massive datasets. They utilize a transformer architecture, which includes neural networks composed of an encoder and a decoder with self-attention mechanisms. These components work together to derive meaning from text sequences and comprehend the relationships between words and phrases.
- Stable Diffusion is a generative AI model that creates distinctive photorealistic images based on text and image prompts.
- Multimodal models are AI systems that can process and generate content across multiple modalities, such as text, images, and audio. These models are designed to understand and integrate information from diverse data types, enabling more comprehensive and contextually rich outputs.
- Researchers introduced the term “foundation model” to describe machine learning models that are trained on a diverse range of generalized and unlabeled data. These models are capable of performing a wide array of tasks, including language comprehension, text and image generation, and natural language conversation. Can be fine-tuned for a wide range of tasks.

## Prompt engineering techniques
- Zero-shot prompting is a technique where a user presents a task to a generative model without providing any examples or explicit training for that specific task. Instead, it relies solely on the general knowledge acquired during pre-training to perform the task based on the prompt.
- Few-shot prompting is a technique that involves providing a language model with contextual examples to guide its understanding and expected output for a specific task. This is technique is particularly helpful for models with limited training data or when adapting the model to new domains or tasks.
- Chain-of-thought (CoT) prompting is a technique that divides intricate reasoning tasks into smaller intermediary steps. This technique can help the model reason through the task in a structured manner and improve its ability to handle complex tasks.
- Self-refine prompting is a technique where a model iteratively solves a problem, critiques its own solution, and then revises the solution based on the critique. This cycle continues until a predetermined stopping condition, such as running out of tokens or time, is met.

## Foundational models fine-tuning
- Instruction-based fine-tuning is a process where a pre-trained foundation model is further trained with specific instructions to perform particular tasks. This approach helps the model understand and follow detailed guidance, generating more accurate and relevant responses. By fine-tuning the model with task-specific instructions, the model becomes capable of handling complex tasks, such as multi-turn conversations or generating personalized recommendations based on user input. This method uses the model's existing knowledge while refining its ability to execute specific tasks, making it ideal for scenarios that require detailed, task-oriented responses.
- Domain adaptation fine-tuning uses a pre-trained model to improve its performance only in a specific domain. This method is more about making the model knowledgeable in a specific domain.

## Core dimension of responsible AI
- Transparency: Refers to the ability to understand and inspect the inner workings, decision-making processes, and outputs of an AI system. It involves making the AI system's behavior, decisions, and underlying logic visible and comprehensible to relevant stakeholders, such as developers, regulators, and end-users.
- Explainability: Providing clear explanations and interpretability of how AI systems make decisions, enabling accountability and trust.
- Veracity and Robustness: Ensuring AI systems operate reliably and consistently and are resilient to potential failures or adversarial attacks.
- Fairness: Ensuring AI models are unbiased and do not discriminate against individuals or groups based on protected characteristics.
- Privacy and Security: Safeguarding the privacy and security of the data used by AI systems and handling personal information responsibly.
- Governance: Establishing clear governance frameworks, policies, and processes for the responsible development and deployment of AI systems.
- Safety: Identifying and mitigating potential risks and unintended consequences associated with AI systems.
- Controllability: Maintaining appropriate human control and oversight over AI systems, particularly in high-stakes decision-making scenarios.

## Generative AI models security vulnerabilities
- Prompt Injection involves manipulating the AI model's input prompts to cause it to produce unintended or harmful outputs. It is crucial to address this vulnerability to prevent malicious users from exploiting the model's behavior.
- Training data poisoning involves attackers manipulating the training data to corrupt the AI model's learning process. This vulnerability can significantly impact the model's accuracy and reliability, making it a critical concern.
- Model theft involves unauthorized access or copying of the model's parameters or architecture. This can lead to misuse of the model or unauthorized replication, which poses a severe risk to the model's intellectual property and security.

## Machine-learning techniques
- Regression is a supervised learning technique used for predicting continuous values. It involves determining the relationship between a dependent variable and one or more independent variables. By analyzing the patterns in historical data, regression models can predict future outcomes, making it ideal for tasks like forecasting stock prices, real estate values, or portfolio performance.
- Linear regression refers to supervised learning models that use one or more inputs to predict a value on a continuous scale. It is used to predict housing prices. After training a model using a set of historical sales training data that includes those characteristics, you could forecast the price of a property based on its location, age, and number of rooms.
- Probability density is generally used to estimate the likelihood or possibility of a random variable falling within a particular range of values, not for predicting future values based on historical data.
- Dimensionality reduction is is primarily used to reduce the number of features in a dataset while retaining as much information as possible. It is not used for prediction tasks directly.
- Anomaly detection is is only used to identify outliers or unusual patterns in data.

## Machine learning approaches
- Supervised Learning is a machine learning approach where a model is trained on a labeled dataset. This means the dataset contains input-output pairs where the desired output is known. The key advantage of Supervised Learning is that it allows the model to learn the relationship between input features like product categories and prices and output label return status, which enables accurate forecasting of future events.
- Few-shot learning is only used when the data available for training is limited. It enables models to generalize from just a few examples.
- Transfer learning is generally used when you have a pre-trained model that can be fine-tuned on a specific task.
- Unsupervised learning is only used for analyzing and clustering data without labeled outputs. It is often applied in scenarios where the goal is to discover hidden patterns or groupings within the data, such as customer segmentation or anomaly detection.

## Unsupervised learning
- Clustering: grouping similar data points together.
- Association rule learning: discovering associations between different features.
- Probability density estimation: estimating the probability distribution of the data.

## Foundational models capabilities
- Visual comprehension: It has the capability to identify objects, scenes, and other elements within images.
- Language processing: It can answer natural language questions and even write short scripts or articles in response to prompts.
- Speech to text: It is designed for tasks like transcription and video captioning in various languages.

## Metrics for evaluation of model results
- Recall-Oriented Understudy for Gisting Evaluation (ROUGE-N) is the most appropriate metric for evaluating text summaries because it is specifically designed for this purpose. It measures how much of the important information from the reference summary is captured in the generated summary, which is essential for determining the effectiveness of a summarization model.
- BLEU (Bilingual Evaluation Understudy) is more commonly used for evaluating machine translation. It measures precision by comparing the n-grams of the generated text with the reference.
- F1 score is a general metric for evaluating classification models, balancing precision and recall.
- Cross-Entropy Loss is a metric used during the training phase of a model to measure the difference between the predicted and actual outputs. It is a tool to optimize model performance during training.
- MAPE (Mean Absolute Percentage Error) calculates the average of the absolute differences between actual and projected values, divides it by actual values, and returns a percentage. A lower MAPE score indicates greater model performance because the predictions are more accurate and closer to the actual values.
- MAE (Mean Absolute Error) is the average difference between expected and actual values for all observations. It is a widely used statistic in numerical prediction tasks to evaluate a model's prediction error. MAE computes the average absolute distance between predicted and actual values, making it simple to interpret. MAE is calculated by combining the absolute errors and dividing by the total number of observations. MAE values range from 0 to infinity, with lower values suggesting a better fit of the model to the dataset.
- Mean squared error (MSE) is primarily used in regression tasks to measure the difference between predicted and actual numerical values. It is not designed to evaluate text similarity.
- Accuracy is a commonly used metric to evaluate the performance of classification models. ( ( TP + TN ) / TOTAL )
- Recall measures the proportion of actual positive instances (true positives) correctly identified by the model.
- InferenceLatency only measures the time taken for a model to generate predictions.
- Perplexity is a metric used to evaluate the performance of language models, typically measures how well a language model predicts the next word in a sequence.
- BERTScore is a tool that compares how similar generated text is to a reference by understanding the context of words leveraging BERT (Bidirectional Encoder Representations from Transformers) embeddings. This makes it better at judging the quality of text, especially for tasks like evaluating chatbots. It helps determine how closely a chatbot's responses match what a human might say or respond.
- Metric for Evaluation of Translation with Explicit ORdering (METEOR) evaluates text similarity based on precision and recall metrics.
- Area Under the ROC Curve (AUC): A performance metric for classification models, representing the model's ability to distinguish between classes across various thresholds.
accuracy = (TP + TN) / TOTAL (for balanced classes)
precision = TP / (TP + FP) (to minimize false positive, like spam,  how often the positive predictions are correct?)
recall = TP / (TP + FN) (to minimize false negatives, like health problems detection, can an ML model find all instances of the positive class?)
false positive rate = FP / (TN + FP)
true negative rate = TN / (TN + FP)
F1 balances precision y recall = (precision * recall) / (precision + recall) * 2

## Visualizations to evaluate model performance
- Confusion matrix: It has entries for all possible combinations of correct and incorrect predictions, and shows how often each one was made by our model.
- Box plot: Typically used to display the distribution of numerical data and highlight measures like the median and interquartile range. 
- Correlation matrix: Shows the linear relationships between numerical variables, which can aid in feature selection.
- Precision-recall curve: Appropriate for binary classification tasks, particularly when there is a class imbalance.

## RLHF (Reinforcement Learning from Human Feedback)
Is a specific technique used in training AI systems to appear more human, alongside other techniques such as supervised and unsupervised learning. First, the model's responses are compared to the responses of a human. Then, a human assesses the quality of different responses from the machine, scoring which responses sound more human. The score can be based on innately human qualities, such as friendliness, the right degree of contextualization, and mood.
One of the key steps in the RLHF approach is creating a reward model. The reward model is trained on human feedback to learn to predict the quality or appropriateness of the language model's outputs. Another key step in the RLHF approach is fine-tuning the language model using the reward model and reinforcement learning techniques.

## ML Algorithms
- Forecasting algorithms are crucial in predictive analytics, especially for predicting future values based on historical patterns in time series data. AWS offers strong forecasting capabilities through Amazon Forecast, a fully managed service that utilizes machine learning to provide accurate time-series predictions. Amazon Forecast automatically manages the complexities of selecting and fine-tuning the appropriate algorithms based on the input data, making it an ideal solution for businesses seeking to enhance their financial planning and resource allocation.
- Linear Learner algorithm is typically used for tasks involving finding a linear relationship between input features and target variables, typically for regression tasks. While it can be used for time series data, it may not effectively capture the temporal dependencies and patterns.
- Object2Vec algorithm is primarily used for creating embeddings for objects or entities so that similar objects are closer in the vector space. This is useful for tasks like recommendations or similarity-based queries.
- Clustering algorithm is only used for grouping similar data points into clusters.

## AWS Cloud Adoption Framework (CAF) key capabilities needed for effective AI integration
- Business: Ensures AI investments drive digital transformation and business outcomes, positioning AI strategically.
- People: Connects AI technology with business, focusing on talent, language, and culture for competitive advantage.
- Governance: Manages AI initiatives to maximize benefits and minimize risks, emphasizing responsible AI use.
- Platform: Builds scalable cloud infrastructure for AI services and development, highlighting AI-specific needs.
- Security: Ensures data and cloud workload security. Addressing AI-specific security challenges.
- Operations: Manages AI workloads to meet business needs, ensuring reliability and consistent value creation.

## Fitting
- Low bias and high variance suggests that the model is too sensitive to the unique properties of the training data. As a result, it fails to generalize successfully to new data—a classic indicator of overfitting.
- Low bias and low variance typically means the model fits the training data well and generalizes well to the test data.
- Increased bias and less variance suggests underfitting, where the model fails to capture the complexity of the data, leading to poor performance on both training and test data.
- Increased bias and increased variability represents underfitting (due to high bias) and overfitting (due to high variance), leading to poor overall performance.

## Concepts
- Data augmentation is a technique for expanding a dataset by generating new samples from existing data through various transformations. This technique addresses challenges in acquiring diverse real-world data by artificially increasing the dataset's size and variety, with recent advances in generative AI enhancing its efficiency and quality.
- Bidirectional Encoder Representations from Transformers (BERT), a bidirectional model, examines the context of an entire sequence before making predictions. It was trained on a plain text corpus and Wikipedia, utilizing 3.3 billion tokens (words) and 340 million parameters. BERT is capable of answering questions, predicting sentences, and translating texts.
- Exploratory Data Analysis (EDA) is the process of analyzing and understanding the characteristics of the data before building an ML model. It involves tasks such as visualizing data distributions, calculating summary statistics, identifying missing values, and detecting outliers. EDA aims to gain insights into the data and identify potential issues or patterns that may impact the model's performance.
- Amazon EC2 Trn1 Instances are specifically designed for high-performance machine learning (ML) model training and utilize AWS Trainium chips. Trainium is a custom-built silicon by AWS optimized for deep learning workloads, making it cost-efficient and scalable for training large and complex models. These instances support major ML frameworks such as PyTorch, TensorFlow, and Apache MXNet, making them versatile for ML practitioners. The Trn1 instances offer high network throughput and fast interconnects, which improve the efficiency of distributed training workloads and reduce overall training time.
- Low bias: Indicates that the model is not making erroneous assumptions about the training data.
- High variance: Indicates that the model is paying attention to noise in the training data and is overfitting.














## AWS Services
- AWS AI Service Cards: provide important information on the ethical considerations, transparency, and intended usage of AWS AI services. They aimed at helping users comprehend the ethical use of AI services, ensuring that the models are fair, transparent, and accountable. These cards provide information on possible hazards and the best ways to use AI services responsibly.
- Amazon Comprehend: is a natural language processing (NLP) service that uses machine learning to find insights and relationships in text.
- Amazon Polly: is a service that turns text into lifelike speech.
- Amazon Textract: is a machine learning service designed to automatically extract text (including handwriting) and structured data from scanned documents.
- Amazon Transcribe: is an automatic speech recognition service.
- Amazon Lex: is for building conversational interfaces using voice and text. It is used to create chatbots that can interact with users through natural language. Additionally, it focuses on dialogue management and natural language understanding.
- Amazon Q Business: is a generative-AI powered assistant designed primarily for enterprises to answer questions, provide summaries, generate content, and automate tasks using their own data sources.
- Amazon Personalize: is a service that only provides personalized recommendations and user experiences by analyzing user behavior and preferences. It is primarily used to create recommendations for applications such as e-commerce or content platforms.
- Amazon Rekognition: is primarily used for image and video analysis, including face recognition, object detection, and content moderation.
- Amazon Kendra: is an enterprise search service that enables users to search a wide range of document formats and data sources. While Kendra can be integrated into a search system to help locate relevant content, it does not perform image analysis or text extraction from images or scanned PDFs.
- Amazon SageMaker: allows you to train your own ML algorithms.
- Amazon Augmented AI (Amazon A2I): is a service that makes it easy to build human review workflows for machine learning predictions. It allows developers to incorporate human review into their machine learning applications to improve model accuracy and ensure compliance with regulatory or business requirements. With Amazon A2I, developers can create human review workflows, manage the workforce, and integrate human review into their applications.
- Amazon OpenSearch Service: makes it easy for you to perform interactive log analytics, real-time application monitoring, website search, and more. For vector databases, you can read about k-Nearest Neighbor (k-NN) search in OpenSearch Service.
- Amazon Aurora PostgreSQL-Compatible Edition and Amazon Relational Database Service (Amazon RDS) for PostgreSQL: support the pgvector extension to store embeddings from machine learning (ML) models in your database and to perform efficient similarity searches.
- Amazon Neptune ML: is a capability of Neptune that uses Graph Neural Networks (GNNs), an ML technique purpose-built for graphs, to make easy, fast, and more accurate predictions using graph data.
- Amazon MemoryDB: supports storing millions of vectors, with single-digit millisecond query and update response times, and tens of thousands queries per second (QPS) at greater than 99% recall.
- Amazon DocumentDB (with MongoDB compatibility): supports vector search, a new capability that enables you to store, index, and search millions of vectors with millisecond response times. With vector search for Amazon DocumentDB, you can simply set up, operate, and scale databases for your ML applications.
- AWS CloudTrail: is a service provided by AWS that enables you to audit, govern, and ensure compliance within your AWS account. Events are recorded in CloudTrail to capture actions performed by users, roles, or AWS services. These events encompass actions carried out in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs. CloudTrail is automatically active in your AWS account upon its creation. Any activity in your AWS account is then logged as a CloudTrail event.
- Amazon Macie: uses machine learning to automatically discover sensitive data within your S3 buckets. It scans objects and identifies patterns that match common types of sensitive information, such as personally identifiable information (PII), credit card numbers, and intellectual property.
- Amazon GuardDuty: analyzes event logs (e.g., CloudTrail, VPC Flow Logs) to detect suspicious activities, unauthorized access, and potential security threats. It focuses on identifying malicious behavior.
- Amazon Inspector: assesses the security posture of EC2 instances, Lambda functions and ECR images. It identifies vulnerabilities, security issues, and potential misconfiguration.
- Amazon Kinesis: is primarily used for ingesting, processing, and analyzing large volumes of real-time data (e.g., logs, clickstreams, sensor data).
- VPC Gateway Endpoint is a highly available and scalable AWS service that allows you to privately connect your Amazon Virtual Private Cloud (VPC) to supported AWS services, including Amazon S3 and Amazon SageMaker, without the need for an internet gateway, NAT device, or VPN connection.
- AWS PrivateLink: allows you to connect your VPC directly to AWS services without exposing your data to the public internet. This is important for businesses that must meet strict compliance standards, as it keeps your network traffic completely private and within the AWS network without relying on public-facing gateways or external connections.
- AWS Artifact: is a self-service portal that provides access to on-demand AWS compliance documentation. This service offers a comprehensive repository of AWS's security and compliance reports, including certifications, attestations, and agreements. These documents are essential for customers in highly regulated industries, such as healthcare, finance, and biotechnology, as they prove AWS's adherence to industry standards and regulatory requirements. AWS Artifact helps organizations ensure that their data hosted on AWS complies with frameworks like HIPAA, GDPR, and PCI DSS.
- AWS Config: is used for assessing, auditing, and evaluating the configurations of your AWS resources.
- AWS Trusted Advisor: is primarily designed to provide real-time best practices guidance to help you optimize your AWS environment.
- Amazon Q Developer: provides AI-powered solutions to help developers increase productivity by automating important coding processes such as generating code samples, tracking references, and ensuring compliance with open-source licensing. By automating these repetitive operations, developers can concentrate on more complicated and inventive elements of software development, lowering the chance of licensing breaches.

### SageMaker features
 - Amazon SageMaker JumpStart: provides an easy way to start with pre-built models and solutions, allowing the company to accelerate its machine-learning efforts without needing extensive expertise. JumpStart offers access to a wide variety of pre-trained models and end-to-end solutions that can be quickly deployed and customized, making it ideal for a company with limited data science resources.
- Amazon SageMaker Data Wrangler: simplifies the process of preparing and transforming data for machine learning. It offers a visual interface for data wrangling, enabling users to clean, transform, and visualize data without writing complex code. This makes it a perfect match for the company's requirement of a low-code solution.
- Amazon SageMaker Canvas: is a no-code tool that enables users to build machine-learning models by simply interacting with data. It allows business analysts and non-technical users to generate accurate predictions without needing to write a single line of code, addressing the company's need for a no-code solution to improve churn prediction.
- Amazon SageMaker Clarify: is designed to detect bias in machine learning models and explain model predictions.
- Amazon SageMaker Model Monitor: is just intended to monitor machine learning models in production to detect data drift and ensure model quality over time.
- Amazon SageMaker Studio Lab: is a free service primarily aimed at learning and experimenting with machine learning using Jupyter notebooks. While useful for educational purposes and early-stage experimentation, it is not designed to offer a low-code or no-code solution suitable for production-level tasks.
- Amazon SageMaker Feature Store: is primarily a centralized repository for storing and managing features used in machine learning models. It allows users to share and reuse features across different models.
- Amazon SageMaker Model Cards: provide a structured framework for documenting essential details about your machine-learning models at every stage of their development. These cards contain information about the model's purpose, training data, evaluation metrics, ethical considerations, and deployment environment. Creating detailed documentation for each model helps organizations adhere to industry standards for transparency and compliance. Model Cards are handy during audits, ensuring all relevant information is documented and easily accessible and facilitating regulatory reviews and internal assessments.
- Amazon SageMaker Ground Truth: is mainly used for creating high-quality labeled datasets through human review workflows.
- Amazon SageMaker Debugger: is just a tool for monitoring and debugging machine learning models during training.
- Amazon SageMaker Training: is a fully managed machine learning (ML) service provided by SageMaker. It helps you effectively train a wide range of ML models at scale. The main components of SageMaker jobs are the containerization of ML workloads, and the management of AWS compute resources. The SageMaker Training platform handles the heavy lifting involved in setting up and managing infrastructure for ML training workloads. With SageMaker Training, you can focus on developing, training, and fine-tuning your model.
- Amazon SageMaker Autopilot: is an automated machine learning solution that can train and deploy models.
- Amazon SageMaker Model Registry: is designed specifically to manage machine learning models.

#### SageMaker Clarify
Amazon SageMaker Clarify, which includes using Partial Dependence Plots (PDPs), helps visualize the impact of different features on a model's predictions. This allows stakeholders to better understand each feature's role in the model's decision-making process, enhancing overall model transparency.
Amazon SageMaker Clarify generates partial dependence plots (PDPs) to display the marginal effect of features on a machine learning model's predicted outcome. These plots help explain the target response with specific input features. Clarify also extends explainability to both computer vision (CV) and natural language processing (NLP) by utilizing the same Shapley values (SHAP) algorithm that is used for explaining tabular data models.

#### SageMaker inference options
- Real-time Inference: Use for low-latency workloads with predictable traffic patterns that need consistent latency characteristics and are always available.
- Serverless Inference: Ideal for synchronous workloads with spiky traffic patterns that can tolerate latency variations.
- Batch Inference: Choose for processing large sets of data offline without requiring a persistent endpoint.
- Asynchronous Inference: Typically used for asynchronous processing where latency is less critical. It helps in cost control by scaling down instances when not in use, which is beneficial for cost-sensitive scenarios.

#### SageMaker built-in options
- Model Parallelism is a feature designed to help train large deep-learning models that cannot fit into the memory of a single GPU. This feature automatically partitions the model across multiple GPUs, efficiently training very large models. By distributing the model layers across different GPUs, SageMaker Model Parallelism enables the more effective utilization of memory and computational resources. This distribution helps reduce the training time and allows for handling models that are otherwise too large to be trained on a single GPU.
- Managed Spot Training is designed to reduce the cost of training jobs by utilizing spare EC2 capacity at a lower price compared to on-demand instances. Thus, Managed Spot Training focuses on cost-efficiency rather than the distribution of large models across multiple GPUs, making it irrelevant to the problem of training very large models.
- Incremental Training enables a model to be further trained with additional data, leveraging previously learned weights. This method is beneficial for updating a model with new data without retraining from the beginning.
- Pipe Mode option optimizes the input data pipeline by streaming data directly from Amazon S3 to the training instances. This helps to efficiently handle large datasets by reducing data loading times and improving the overall throughput of the training process.

#### Amazon SageMaker Pipelines step
- CreateModel: This step creates a deployable SageMaker model from the trained artifacts, preparing it for inference in a production environment.
- Training: It handles training the machine learning model using the prepared data, generating the model artifacts needed for deployment.
- QualityCheck: This step evaluates the model to ensure it meets performance and quality standards before being deployed.
- Processing: It preprocesses and transforms raw data into a suitable format for model training.

#### Train a model in SageMaker Training from S3 data
- Upload the dataset to Amazon S3.
- Create a training job in Amazon SageMaker.
- Configure the training job to use the dataset from Amazon S3.

### Amazon Bedrock features
- Model Evaluation on Amazon Bedrock: enables you to assess, compare, and choose the most suitable foundational models for your specific needs. Amazon Bedrock provides the option of automatic evaluation and human evaluation. You can utilize automatic evaluation with predefined algorithms for metrics like accuracy, robustness, and toxicity. Moreover, for subjective or custom metrics such as friendliness, style, and alignment to brand voice, you can establish a human evaluation workflow with just a few clicks. Human evaluation workflows can make use of your own employees or an AWS-managed team as reviewers. Model evaluation offers preselected curated datasets or allows you to bring your own datasets.
- Amazon Bedrock Guardrails: allow you to set up protections for your AI applications, aligning with your specific use cases and responsible AI guidelines. You can customize multiple guardrails for various scenarios and apply them to different foundation models (FM), ensuring a uniform user experience and consistent safety and privacy measures across your AI applications. These guardrails can be used with both user inputs and model responses based on text.

#### Customize a foundational model using Amazon Bedrock
- Prepare the training dataset
- Create a fine-tuning or pre-training job
- Purchase Provisioned Throughput

### Amazon Rekognition features
- Content moderation is the process of monitoring and filtering user-generated content to ensure it complies with the platform's policies and guidelines. It involves detecting and removing explicit, offensive, or inappropriate content.
