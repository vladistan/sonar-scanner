# Sonarqube Scanner

The SonarQube Scanner

```
docker pull gcanal/sonar-scanner
```

## Build your own image 

```bash
docker build -t company/sonar-scanner .
```

You can although build the image using a specific sonar-scanner version like so :

```bash
docker build --build-arg SONAR_SCANNER_VERSION=3.0.1.733 -t company/sonar-scanner:3.0 .
```

## Use the image

Assuming you have a SonarQube instance running inside a Docker container named `sonarqube` : 

```bash
docker run --rm -it -v $(pwd):/app --link sonarqube:sonarqube gcanal/sonar-scanner -Dsonar.host.url=http://sonarqube:9000
```

## SonarQube up and running

### Your own Sonarqube instance

This project provide a docker compose file that provide an official sonarqube instance running against a postgres database.

Just run `docker-compose up -d`

You may be interested in reading [the documentation](https://github.com/SonarSource/docker-sonarqube) from the official dockerized SonarQube image.

## Configure your project

You will need to create a `sonar-project.properties` at your project root with the following :

```
sonar.projectKey=vendor:project-name
sonar.projectName=MyProject
sonar.projectVersion=1.0
sonar.language=a_language
sonar.sources=src
sonar.sourceEncoding=UTF-8
```

- replace `vendor:project-name` will a relevant project key (ex : `company:awesome-project`)
- replace `MyProject` with a project name (ex : `AwesomeProject`)
- replace `1.0` with a [meaningful version number](http://semver.org)
- replace `a_language` with a supported SonarQube language (ex : `php`)
- replace `src` with the relative path to your source code

Depending of the language specified in `sonar.language`, more parameters may be available to you, please read [Analyzing with SonarQube Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner)

