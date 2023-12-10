# OpenTelemetry demo

This repo serves to illustrate the very basics of instrumenting a simple Flask app using OpenTelemetry

#### Run the Collector

Grab the docker image: `docker pull otel/opentelemetry-collector-contrib`

Run it, opening the required ports:
- OTLP receiver on 4317
- zPages at 55679 (dunno what that is)
- metrics endpoint on 8888 (browse at `...:8888/metrics)

Redirect `stderr` to a file if you want to look at it later.

```
docker run -v $(pwd)/collector-config.yaml -p 0.0.0.0:4317:4317 -p 127.0.0.1:55679:55679 -p 0.0.0.0:8888:8888 otel/opentelemetry-collector-contrib  2> collector.logs
```

#### Run Flask instrumented

```
OTEL_EXPORTER_OTLP_INSECURE=true opentelemetry-instrument flask run 
```

# Riddle Me This Game

### Description

In this project I created a simple website with the usual HTML, CSS, Javascript for the front end and Python and Flask for the back end.

The user is required to input their name to start the game, once in, you get asked 10 riddles.
The maximum score per riddle is 3 points.
You get 3 guesses per riddle. As you use up your guesses, 1 point is subtracted from that score so if you get one wrong guess you will get 2 points, two wrong guesses is 1 point and three wrong guesses is gameover.
Once the user makes it to the end of the 10th riddle, their score will be added into the highscore file and if they make the top 10, they will be added to the highscore page.

The site was made using VS Code and Cloud 9 IDE and tested using Google Chrome, Mozilla Firefox and Internet Explorer. Several Android devices as well as an iPhone 6s were also used in the testing process. Google Chrome inspector was used to simulate several device screen sizes I could not personally get my hands on.

Mockups can be found in the /mockup/ folder in this Git repo.


### The following is a table on the functionality of the site.

| Page/Feature | Description |
| :--- | :---: |
| Homepage | Extremely simple, asks for a username in order to continue to the game |
| Welcome | This is a small page welcoming the user with some rules |
| About | Quick about page with little info |
| Highscore | This is where the highscores are kept and viewed |
| Game | The meat of the project, where all the fun happens |
| Gameover | If you lose, you will be redirected to this page |
| Congratulations | If you win, you will be redirected to this page |


### Below is a list of Libraries/Technologies that were used in the creation of this website:

* [Flask Micro Framework](http://flask.pocoo.org/)
Flask provides an interface between Python and the web. It is used for all the logic on the site.
* [Bootstrap CSS Framework](https://getbootstrap.com/)
This framework was used throughout the website on all pages to facilitate a responsive design.
* [FontAwesome Icons](https://fontawesome.com/)
Used for the Social Media icons and the Media button.

### Deployment

The project is deployed on Heroku, you can reach it by going to this [link](https://shaun-riddle-game.herokuapp.com/)

There is a slight problem with beginning a game that doesnt always happen. Once the user inputs a Username to play the game then clicks on the 'Play' button, there is a possibility of getting a server error. To get past this, press the back button on the browser and then click 'Play' again. Keep trying that until it works.