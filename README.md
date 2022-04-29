# practicing-dmn-lab03 starter Project
Run on quarkus dev mode: 
```
mvn quarkus:dev 
```

## How to use via rest:

POST http://localhost:8080/DecisionWithJava
{
  "Names": ["John Doe","Ash"]
}

POST http://localhost:8080/CanParty
{
    "Guest": {
        "birthdate": "1980-01-01",
        "name": "Karina V"
    },
    "Planned date": "2021-10-25"
}


## Serverless deployment

Compile on native mode
```
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

Create a new image with the native executable (replace the url with your own)
```
docker build -f src/main/docker/Dockerfile.native -t quay.io/kvarel4/serverless-decision-demo:1.0 .
```

Push to quay
```
docker push quay.io/kvarel4/serverless-decision-demo:1.0
```

Deploy with knative (requires openshift and knative serving):
```
oc new-project serverless-decision-demo
kn service create serverless-decision --image quay.io/kvarel4/serverless-decision-demo:1.0
kn service list
```