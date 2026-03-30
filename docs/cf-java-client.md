# Running integration tests of cf-java-client

This guide explains how to run the integration tests of [cf-java-client](https://github.com/cloudfoundry/cf-java-client) on kind-deployment.

## 1. Clone branch cf-java-client.integration-test of project [kind-deployment](https://github.com/cloudfoundry/kind-deployment)
In this branch there are some minor changes to the configuration of CF that are required by the integration
tests but should not be part of the default configuration. Mainly that is the existence of an admin user with
known password and a client with admin rights and known password.

## 2. Install kind-deployment as documented

## 3. Start CF
```bash
make up
make login
make bootstrap-complete
```

## 4. Set environment for integration-tests of cf-java-client
```bash
source ./settings.sh
```

## 5. Clone [cf-java-client](https://github.com/cloudfoundry/cf-java-client)
Clone cf-java-client to a different directory and cd to that directory.
Set up the project as described [there](https://github.com/cloudfoundry/cf-java-client#development).

Build the project once to see if setup is correct.
```bash
$ git submodule update --init --recursive
$ ./mvnw clean install
```


## 6. Run the integration-tests
```bash
./mvnw -Pintegration-test clean test -Dtest=org.cloudfoundry.client.v3.ServiceBrokersTest#update
```
