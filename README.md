## Getting stated with Gemini Pro
This sample project shows how to connect to Google's [Gemini Pro](https://cloud.google.com/vertex-ai/docs/generative-ai/model-reference/gemini) API through [Vertex AI](https://cloud.google.com/vertex-ai?hl=da). We want to go through Vertex AI because Denmark is not a [supported region](https://ai.google.dev/available_regions#available_regions) at the time of writing (25-02-2024). 

So, to make it work, we circument the region restriction by setting the location to `us-central1` in the Vertex AI client. Like so:

```python
import vertexai

vertexai.init(
    project=project, # our GCP project
    location="us-central1", # <- magic hack
    credentials=creds # our IAM credentials (JSON)
) 
```

### Purpose
All new sign-ups to Google Cloud recieve 300$ in free credits. You will have to put in a credit card, but you will **not** be automatically billed if you run out of token. This makes it a great way to get started with LLMs (and other cool stuff on Google Cloud)

### Setting up your Vertex AI / GCP project

To get started with Vertex AI, you need to 
- Create a new account in Google Cloud (for the free credits. You should use your CBS email)
- Set up a new project in Google Cloud. 
- Enable the Gemini Pro API
- Create a service account
- Download the service account credentials as a JSON file

We use this service account credentials JSON file to authenticate with the Gemini Pro API in our Python code.

Here is a step by step guide: 
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create an account if you don't have one. (If you do have one, create a new account, since we need the cedits).
3. Create a new project (say, 'my-aiml24')
4. Follow this guide https://youtu.be/I8W-4oq1onY?si=rIybghWBmKgB8nXH&t=99 (from 1:39 to 4:00) to enable Vertex AI API
(Everything from 4:00 onwards is not needed for this project)
5. When we have the `service_acc_key` JSON file, place it in the root of this project. Like so

``` bash
.
├── README.md
├── example_service_acc_key.json
├── notebooks
│   └── prompting.ipynb
├── conda.yaml
└── service_acc_key.json # <- place it here
```

### Setting up your Python environment
Now, I'm assuming you have Python and Anaconda/conda installed. If not, go to [python.org](https://www.python.org/downloads/) and download the latest version of Python. Then, go to [anaconda.com](https://www.anaconda.com/products/distribution) and download the latest version of Anaconda. (YouTube is your friend if you need help with the installation - Otherwise ask through Canvas or during the exercise lab)

Now, open a terminal and navigate to the root of this project. Then, run the following commands to create your virtual environment and install the required packages.

``` bash
# create the environment
conda env create -f aiml24-gemini.yml --prefix=aiml24-gemini
```
This will create a conda environment called `aiml24-gemini` with all the required packages in the root of this project. This is useful because VSC etc. will pick it up automatically.

``` bash
# activate the environment - This should output a bunch of stuff
conda activate /some/path/to/your/project/aiml24-gemini
```
A directory called `aiml24-gemini` should now be created in the root of your project. This is where all the packages are installed. Then, if you are using [Jupyter Notebook](https://jupyter.org/), you can run the following command, with the environment activated, to open Jupyter Notebook in your browser:

``` bash
jupyter notebook
```

You should also be able to open [Visual Studio Code directly from Anaconda Navigator](https://docs.anaconda.com/free/working-with-conda/ide-tutorials/vscode/) and then [upload the aiml24-gemini environment from there](https://server-docs.anaconda.com/en/latest/user/environment.html). You can of course also use any other Python IDE you like, but I recommend Visual Studio Code

**Note**: If this is overwhelming, don't worry. You will have plenty of time to ask about it in the exercise lab.

### Running the code
Assuming your environment is set up properly, you should be able to run the code in the `notebooks/prompting.ipynb` file. This is an Ipython notebook file which runs brilliantly in Visual Studio Code and, of course, Jupyter Notebook. Select your environment from the top right corner of VSC and run the code.










   