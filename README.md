# Development Workshop - OCEL from EMAIL dataset

We worked on two different email datasets to create Object-Centric Event Logs. 

## Datasets

Hillary Clinton's email dataset: https://www.kaggle.com/datasets/kaggle/hillary-clinton-emails

JIRA email dataset

## Methods used for every Version 

### spaCY.ipynb:
In the first version of the project, we imported the datset and extracted the content of the email from the dataset. Then we preprocess the data and clear the unnecessary stopwords to ease the process. We used the spaCy library to extract verbs and detect the events from the contents. We created a frequency table for visualize the most used verbs in the dataset.

### re_k.ipynb:
First observations and tests on the new dataset(We were planning to use re library but we decided that we would get better results with spaCy library).

### spaCy_k.ipynb:
We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. 

### part_x.ipynb:
We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. We added most common events as predefined variable to our model. In the functions extract_event, extract_object, extract_actor we are extracting the informations to create OCELs, and we create our OCELs by usind ocel_entries function. Some examples from the output we get;

{'Event': None,
  'Object': 'CAMEL-11099',
  'Actor': 'Daniel Fullarton',
  'Timestamp': 'Sun, 02 Apr, 23:59'}

 {'Event': None,
  'Object': 'CAMEL-11099',
  'Actor': 'Daniel Fullarton',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

As clearly seen that even though we get the correct actor, we couldn't get the event and correct objects.

  ### part_x2.ipynb:
  We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. By using nltk library we removed unnecessary characters, symbols, stopwords, and punctuations. Then we tokenized the lemmatized words. We added the most common events as predefined variables to our model, but this time it covers more events than the previous version. In the functions, extract_event, extract_object, and extract_actor we are extracting the information to create OCELs, and we create our OCELs by using the ocel_entries function. Some examples from the output we get;

  {'Event': 'create',
  'Object': None,
  'Actor': 'daniel fullarton',
  'Timestamp': 'Sun, 02 Apr, 23:59'}

 {'Event': 'resolve',
  'Object': None,
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Event': 'merge',
  'Object': None,
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

As clearly seen even though we get the correct actors, timestamps, and unlike the previous version we get the correct actor but we still couldn't extract the correct object from the content.

### part_x3.ipynb:
We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. By using nltk library we removed unnecessary characters, symbols, stopwords, and punctuations. Then we tokenized the lemmatized words. Unlike previous versions instead of predefining the events by using the spaCy library we extracted the most used verbs in the dataset and created the event patterns automatically. In the functions, extract_event, extract_object, and extract_actor we are extracting the information to create OCELs, and we create our OCELs by using the ocel_entries function. Additionally, we change the function extract_object to get better results in this version. Some examples from the output we get;

{'Id': 0,
  'Event': 'create',
  'Object': 'create',
  'Actor': 'daniel fullarton',
  'Timestamp': 'Sun, 02 Apr, 23:59'}

 {'Id': 1,
  'Event': 'pull',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'request',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'resolve',
  'Object': 'request',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}


### part_x3.1.ipynb:
We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. By using nltk library we removed unnecessary characters, symbols, stopwords, and punctuations. Then we tokenized the lemmatized words. Unlike previous versions instead of predefining the events by using the spaCy library we extracted the most used verbs in the dataset and created the event patterns automatically. In the functions, extract_event, extract_object, and extract_actor we are extracting the information to create OCELs, and we create our OCELs by using the ocel_entries function. Some examples from the output we get;

{'Id': 0,
  'Event': 'create',
  'Object': 'create',
  'Actor': 'daniel fullarton',
  'Timestamp': 'Sun, 02 Apr, 23:59'}

 {'Id': 1,
  'Event': 'pull',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'request',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'resolve',
  'Object': 'request',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}


  ### part_x3.2.ipynb:
  We used html library to clear unnecessary html snippets in the email body for ease of preprocessing. By using nltk library we removed unnecessary characters, symbols, stopwords, and punctuations. Then we tokenized the lemmatized words. We use natural language processing to figure out the most repeated events/activities on the mail content by extracting the verbs. After observing the verbs we have decided to set the repetition bar to 31. The remaining part of the verbs seems less necessary. We have created event patterns based on the most repeated verbs. 
  
  We have created different functions for the extraction of event log elements.
* In the extract_event function we extract the action based on the event_patterns we have created previously.
* In the exract_object function we have decided to choose a context_window number to detect the possibile nouns (detected by NLP) which could be reffered by the action.
* And finally we wanted to add an extract_actor function to detect names of the actors who has taken the action with again NLP.

We create ocel_entries to store the events with their features by detecting them with NLP, and using functions we have created.

 Some examples from the output we get;

 {'Id': 1,
  'Event': 'request',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'resolve',
  'Object': 'request',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

 {'Id': 1,
  'Event': 'merge',
  'Object': 'pull',
  'Actor': 'asf github',
  'Timestamp': 'Mon, 03 Apr, 00:01'}

  'Event': 'close',
  'Object': 'change',
  'Actor': 'asf github',
  'Timestamp': 'Thu, 13 Apr, 15:21'}


We used pm4py to convert our results to OCEL standard. We are required a date type in the dataframe in order to change our results to OCEL standard. In our dataset year information is not given inside the timestamp column, but all the emails are sent in 2017, so we changed the date manually. We change the 'Object' column into 'ocel:oid' because it is also required for the conversion.In our case, we do not have different type for the objects. So we give all the objects same type 'ocel:oid'. In the end we export our result in the "ocel_file.csv" file as a standart CSV file and "ocel_objects.csv" and "ocel_events.csv" files as OCEL file format.
