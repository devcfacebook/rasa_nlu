# RASA_NLU

### Installation
Es requisito tener instalado al menso `python 2.7`
```
sudo pip install rasa_nlu
sudo apt-get install build-essential libssl-dev libffi-dev python-dev
sudo pip install -U spacy
sudo python -m spacy download es
```

### Training
En este repositorio encontrara dos archivos:
- `config.json`
- `training-data.json`

Estos archvis son necesarios para entrenar a nuestra modelo. Usted puede modificar el archivo de entrenamiento a su discreción.

Para hacerlo debe ejecutar el siguiente comando, desde la carpeta raíz de este proyecto.
```
python -m rasa_nlu.train -c config.json
```

Debe notar que el contenido de este `config.json` es:
```
{
    "language": "es",
    "pipeline": "spacy_sklearn",
    "path" : "projects",
    "data" : "./training-data.json"
}
```

Donde indicamos cosas como: el lenguaje de las oraciones, el archivo de los `training examples`.

### Testing
Una vez entrenado el modelo, usted podrá y deberá apreciar dos carpetas nuevas: `logs` y `projects` que son generadas luego del entrenamiento.

Una vez hecho esto, usted podrá levantar su servicio para poder probarlo:
```
python -m rasa_nlu.server -c config.json
```

Este comando inicia un servidor http ubicado por defecto en el puerto: `5000`

### Response
Puede probarlo haciendo un `HTTP GET` a `http://localhost:5000/parse?q=chiste`, lo cual le deberá retornar algo como:
```
{  
   "entities":[  

   ],
   "intent":{  
      "confidence":0.7127653347715731,
      "name":"chiste"
   },
   "text":"chiste",
   "intent_ranking":[  
      {  
         "confidence":0.7127653347715731,
         "name":"chiste"
      },
      {  
         "confidence":0.2005844024482644,
         "name":"none"
      },
      {  
         "confidence":0.08665026278016225,
         "name":"consejos-amor"
      }
   ]
}
```
