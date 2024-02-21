Quarkus Security with WebAuthn
================

    플리 시.

**:**

1. :
2.     * , ,    보 
3.     *  보  
4.     *  보 DB 
2. Minio 스리 :
3.     *  ,  ID  Minio   
4.     * Minio   보 JSON  
**:**

* 프: React
* * : Quarkus
* * 스:
*     *  스
*     * Minio 스리 스
* * 스: PostgreSQL
* *  스리: Minio
* * : Docker
* * AI :
*     *  리 (  )
*     *   (Quarkus 스   )
** :**

*   Minio 스리   리 스 
* * Docker   스  
* * React     스 
* *  보 PostgreSQL 스 
* * Minio   보 JSON   스리 
* * AI     Minio 스리      
* *  스   
**:**
* Quarkus: https://quarkus.io/
* * Minio: https://min.io/
* * Docker: https://www.docker.com/
* * React: https://reactjs.org/
* * PostgreSQL: https://www.postgresql.org/
**AI   :**
* 스 아  
* * Quarkus  
* * Minio API 
* * React UI  
* * PostgreSQL 스  
** :**
* AI      시 
* *  리 스   보   
* * Docker     
* *    스 
** :**
*  보     
* * Minio  리  
* * 보안   (HTTPS, CSRF  )
**:**
* AI   아       .
* * 보안  안  플리  스 .
* AI  :
Google AI Code Transformer: [  URL ]
* OpenAI Codex: https://openai.com/blog/openai-codex/
* Github Copilot: https://github.com/features/copilot
* AI  :
    AI  
:
 프프 AI   Quarkus  스 플리    시.    시   보    플리   .



Gemini     보 시       .  보 보  Gemini 



      ggggg%yrghg345tcfrrrffg
This guide demonstrates how your Quarkus application can use a database and WebAuthn to store your user credentials.

## Start the database

You need a database to store the user identities/credentials. Here, we are using [PostgreSQL](https://www.postgresql.org).
To ease the setup, we have provided a `docker-compose.yml` file which start a PostgreSQL container and bind the network ports.

The database1 can be started using:
 ```bash
 docker-compose up
 ```

Once the database is up you can start your Quarkus application.

Note you do not need to start the database when running your application in dev mode or testing. It will be started automatically as a Dev Service.

## Start the application

The application can be started using: 

```bash
mvn compile quarkus:dev
```  

## Test the application

### From  the CLI
The application exposes 4 endpoints:
* `/api/public`
* `/api/public/me`
* `/api/admin`
* `/api/users/me`

You can try these endpoints with a browser, using a hardware token by visiting http://localhost:8080. 

### Integration testing

We have provided integration tests based on [Dev Services for PostgreSQL](https://quarkus.io/guides/dev-services#databases) to verify the security configuration in JVM and native modes. The test and dev modes containers will be launched automatically because all the PostgreSQL configuration properties are only enabled in production (`prod`) mode.


The test can be executed using: 

```bash
# JVM mode
mvn test

# Native mode
mvn verify -Pnative
```

## Running in native

You can compile the application into a native binary using:

`mvn clean package -Pnative`

_Note: You need to have a proper GraalVM configuration to build a native binary._

and run with:

`./target/security-jpa-webauthn-1.0.0-SNAPSHOT-runner` 

_NOTE:_ Don't forget to configure and start your database if you run without DEV services.