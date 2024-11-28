# Neurocontrol-of-the-quality-of-managers-conversations

# Conversation Analysis Tool

## Overview

The **Conversation Analysis Tool** is a Python-based project designed to analyze and classify conversations between a manager and a client. The tool is particularly useful for organizations that provide remote training to clients, helping them to understand the dynamics of these interactions. The analysis includes identifying the formal establishment of contact, emotional tones, and personalized interactions that go beyond mere formality.

## Features

- **Conversation Classification**: Classify conversations based on various criteria such as cold calls, warm calls, and administrative calls.
- **Emotional Tone Analysis**: Evaluate the client's emotional tone, including positive, negative, and neutral emotions.
- **Question Analysis**: Count the number of questions from both the manager and the client.
- **Overcoming Objections**: Identify and analyze client objections and the manager's responses.
- **Phrase Length Analysis**: Measure the average phrase length from both parties and the maximum phrase length.
- **Refusal Formulations**: Detect clear client statements indicating final refusal to purchase or collaborate.
- **Conversation Structure**: Analyze the number of topic transitions, conversation duration, and pauses.
- **Additional Features**: Evaluate engagement, persistence, expertise, and personal contact during the conversation.

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/conversation-analysis-tool.git
   cd conversation-analysis-tool
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. **Load Data**:
   - Load the conversation data and label dictionaries using `joblib`.
   ```python
   import joblib
   df_label_new = joblib.load('path_to_label_data.joblib')
   df_label_dict_new = joblib.load('path_to_label_dict.joblib')
   ```

2. **Set Display Options**:
   - Set pandas display options to view the dataframes.
   ```python
   import pandas as pd
   pd.set_option('display.max_columns', None)
   pd.set_option('display.max_colwidth', None)
   ```

3. **Analyze Conversations**:
   - Use the provided system role, pre-text, and post-text to analyze the conversation.
   ```python
   systemrole = 'You are a helpful assistant. Your primary task is to accurately classify and analyze conversations between a manager and a client in Russian. Focus on identifying not only the formal establishment of contact but also any deeper emotional connection or personalized interaction that goes beyond mere formality.'
   predtext = 'The manager works for an organization that provides remote training to clients. The manager calls clients and offers them training programs. Roles in the conversation are always divided as follows: 1) Manager, 2) Client. Here is a conversation that took place in Russian:'
   posttext = ''' Analyze the conversation between the manager and the client. Respond in JSON format. In the "summary" variable, provide a brief summary of the entire conversation in Russian. For variables label1 to label83, record the count of phrases or relevant information based on the following criteria: ... '''
   conversation = ''' ... '''
   response = gpt4(systemrole, predtext + conversation + posttext)
   print(response)
   ```

4. **Evaluate Labels**:
   - Evaluate the labels using a phik matrix and heatmap.
   ```python
   import pandas as pd
   import numpy as np
   from phik import phik_matrix
   import matplotlib.pyplot as plt
   import seaborn as sns

   data_gpt = pd.read_excel('path_to_data_gpt.xlsx')
   phik_matrix_result = data_gpt.phik_matrix(interval_cols=['label' + str(i) for i in range(37, 84) if 'label' + str(i) in data_gpt.columns])
   plt.figure(figsize=(20, 20))
   sns.heatmap(phik_matrix_result, annot=True, cmap='viridis', fmt=".2f")
   plt.title('Phik Correlation Matrix')
   plt.show()
   ```

## Example

Here is an example of how to use the tool to analyze a conversation:

```python
# Load data
df_label_new = joblib.load('data/qq85_stthomeoffice_label2.joblib')
df_label_dict_new = joblib.load('data/qq85_stthomeoffice_label2_dict.joblib')

# Set display options
pd.set_option('display.max_columns', None)
pd.set_option('display.max_colwidth', None)

# Analyze conversation
systemrole = '...'
predtext = '...'
posttext = '...'
conversation = '...'
response = gpt4(systemrole, predtext + conversation + posttext)
print(response)
```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue if you have any suggestions or find any bugs.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

- Thanks to the open-source community for providing the tools and libraries used in this project.
- Special thanks to the contributors who have helped improve this tool.

---

For more details, please refer to the [documentation](docs/README.md).
