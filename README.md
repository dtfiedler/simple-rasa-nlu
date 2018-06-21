# A Simple RasaNLU Http Server

<div align="center">
    <img src="https://rasa.com/assets/img/rasa-ecosystem.png"/>
</div>

## Installation:

Follow the docs to install RasaNLU available [here](https://nlu.rasa.com/installation.html)

## To run:

``` 
git clone git@github.build.ge.com:GSIT/simple-rasa-nlu.git
cd simple-rasa-nlu
python -m rasa_nlu.server --path projects/default
```

## Example Request

Once you have the server running, you can do an example request to the following URL:

http://localhost:5000/parse?q=hello%20there&project=rasaBot

You should see the following response:

```
{
  "entities": [], 
  "intent": {
    "confidence": 1.0, 
    "name": "greet"
  }, 
  "text": "hello there"
}
```


# Adding your own project

## Steps: 
1. Create your own training data using the site available [here](https://rasahq.github.io/rasa-nlu-trainer/)
2. Download the file using the "Download" button in top right as <PROJECT_NAME>-trainging-data.json and save it in the [data](data) directory
3. Update the [config_spacy.json](config_spacy.json) file to:

        {
            "fixed_model_name": "<PROJECT_NAME>",
            "pipeline": "spacy_sklearn",
            "path" : "./projects",
            "data" : "./data/PROJECT_NAME-training-data.json"
        }
4. Run the command (this trains Rasa based on your input)
```
    python -m rasa_nlu.train -c config_spacy.json
```
5. This should create a new folder in the projects/default  directory called <PROJECT_NAME>
6. Rerun your server by running the command: 
```
python -m rasa_nlu.server --path projects/default
```
7. Test one of your example queries by going to 
```
 http://localhost:5000/parse?q=<YOUR_SAMPLE_TEXT>&project=<YOUR_PROJECT_NAME>

```