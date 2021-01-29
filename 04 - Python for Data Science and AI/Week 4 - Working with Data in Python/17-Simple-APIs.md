# Simple APIs
## Simple APIs (Part 1)
### REST APIs

+ Allow communication through the Internet
+ Allow you to take advantage of resources like storage, access more data, AI algorithms, and much more.

 
+ The RE stands for representational. 
+ The S stands for state. 
+ The T stands for transfer

![Image](https://i.imgur.com/UOjlYq0.png)

+ Rules
    + communication
    + input or request
    + output or response


+ methods
    + HTTP method
        ![Image](https://i.imgur.com/wS30PMq.png)

+ Applications
    + [nba_api] at <www.nba.com>

## Simple APIs (Part 2)
### Outline
+ API keys and endpoints
+ Watson Speech to Text
+ Watson Translate

### API Keys and Endpoints
![Image](https://i.imgur.com/KFt4MQW.png)
+ API Key

### Watson Speech to Text
```py
from ibm_watson import SpeechToTextV1
url_s2t = 'https://stream.watsonplatform.net/speech-to-text/api'

iam_apikey_s2t = 'xxxxx'
s2t = SpeechToTextV1(iam_apikey=iam_apikey_s2t, url=url_s2t)

filename='hello_this_is_python.wav'
with open(filename, mode='rb') as wav: # reading the code in the binary format
    response = s2t.recognize(audio=wav, content_type='audio/wav')
    response.result # dictionary
    recognized_text = response.result['results'][0]['alternatives'][0]['transcript']
```

### Watson Translate
```py
from ibm_watson import LanguageTranslatorV3

url_lt = 'https://gateway.watsonplatform.net/language-translator/api'
apikey_lt = 'xxxx'
version_lt = '2021-01-29'
language_translator = LanguageTranslatorV3(iam_apikey=apikey_lt, url=url_lt, version=version_lt)
print(language_translator.list_identifiable_languages().get_result())

recognized_text = 'hello this is python'
trans_response = language_translator.translate(text=recognized_text, model_id='en-es') # english to espanio

translation = trans_response.get_result() # dictionary

es_trans = translations['translations'][0]['translation']
es_trans # str

translation_new = language_translator.translate(text=es_trans, model_id='es-en').get_result()
en_trans = translation_new['translations'][0]['translation']
```

