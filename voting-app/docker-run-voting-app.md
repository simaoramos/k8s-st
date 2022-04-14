# Voting app

- docker run -d --name=redis redis
- docker run -d --name=db postgres:9.4
- docker run -d --name=vote -p 5000:80 --link redis:redis kodekloud/examplevotingapp_vote:v1
- docker run -d --name=result -p 5001:80 --link db:db kodekloud/examplevotingapp_result:v1
- docker run -d --name=worker --link db:db --link redis:redis kodekloud/examplevotingapp_worker:v1