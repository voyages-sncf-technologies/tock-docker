[![Build Status](https://travis-ci.org/voyages-sncf-technologies/tock-docker.png)](https://travis-ci.org/voyages-sncf-technologies/tock-docker)

# Docker images for [Tock](https://github.com/voyages-sncf-technologies/tock)

## Build images

You will need [Maven](https://maven.apache.org/) and [Git](https://git-scm.com/).

```sh 
    git clone https://github.com/voyages-sncf-technologies/tock-docker.git
    cd tock-docker
    mvn package docker:build
```

## Run images

Several docker-compose files are provided.

### NLP stack

```sh 
    docker-compose up
``` 

And go to [http://localhost](http://localhost) to use the admin interface.

### Open Data Bot example

This docker-compose file starts the NLP stack with the [Open Data Bot](https://github.com/voyages-sncf-technologies/tock-bot-open-data). 

* Edit the file [bot-open-data-variables.env](https://github.com/voyages-sncf-technologies/tock-docker/blob/master/bot-open-data-variables.env) and set the required env variables.
 
You will need a (free) [SNCF Open Data key](https://data.sncf.com/) and a Messenger application (look at the [Facebook documentation](https://developers.facebook.com/docs/messenger-platform/guides/quick-start)). 

```sh 
    #Sncf open data api user
    tock_bot_open_data_sncf_api_user=

    #facebook page id
    tock_bot_open_data_page_id=

    #messenger page token
    tock_bot_open_data_page_token=

    #messenger application secret key
    tock_bot_open_data_application_secret=

    #facebook webhook verify token
    tock_bot_open_data_webhook_verify_token=
``` 

* Also to test the bot directly on your desktop, a secure ssl tunnel (for example [ngrok](https://ngrok.com/)) is required:

```sh 
    ngrok http 8080
``` 

* Then run the bot

```sh 
    docker-compose -f docker-compose-bot-open-data.yml up
``` 

* Take the ngrok value (ie  https://xxxx.ngrok.io ) and use it in the webhook interface of messenger settings, to specify :
   * the url : https://xxxx.ngrok.io/messenger
   * the verify token you set in tock_bot_open_data_webhook_verify_token env var

Now you can start to talk to the bot!