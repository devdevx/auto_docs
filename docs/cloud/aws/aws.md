# AWS
## SAM

Commands
````
sam init
sam local start-api
sam local generate event <service> <type> > events/event.json
sam local invoke "<function>" -e events/event.json
sam build
sam deploy
sam deploy --guided
sam delete
````