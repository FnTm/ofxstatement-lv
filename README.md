# Transform statements from Latvian banks to OFX using Docker

If you're using a financial tool like [YNAB](https://http://www.youneedabudget.com/) you know that entering all of your transactions can be a pain. And even though tools like YNAB offer importing transactions directly from your bank, unless you're in US you're probably out of luck.

YNAB allows you to import OFX files which can make this process easier. [OFX Statement](https://github.com/kedder/ofxstatement) is a project that provides a plugin-enabled architecture, where anyone can create a compatible plugin for their local banks.

This project is made possible by [Gints Murāns' OFX parsers for Latvian banks](https://github.com/gintsmurans/ofxstatement-latvian) and
[Miku Laitinen's OFX parser for Revolut](https://github.com/mlaitinen/ofxstatement-revolut). Major kudos!

Supported sources:

- `Swedbank` - CSV files
- `DNB` - FIDAVISTA xml files
- `Citadele` - FIDAVISTA v1.2 xml files
- `SEB` - CSV files
- `Revolut` - Revolut's CSV files

## Usage
 ```
 docker run -v ~/dev/ofx/data:/data fntm/ofxstatement-lv ofxstatement convert -t swedbankLV /data/statement.csv /data/swed.ofx
 ```
The example above assumes that
- You have a folder named data which can be linked as volume to the docker container (needed to give ofxstatement access to that file)
- You have downloaded a .csv statement from Latvian swedbank in said folder

### Example for Citadele
```
 docker run -v ~/dev/ofx/data:/data fntm/ofxstatement-lv ofxstatement convert -t citadeleLV /data/statement.xml /data/citadele.ofx
 ```

### Example for Revolut
```
 docker run -v ~/dev/ofx/data:/data fntm/ofxstatement-lv ofxstatement convert -t revolut /data/revolut.csv /data/revolut.ofx
 ```

## Publishing a new release
1. Tag relevant release commit with release version.
   ```bash
    git tag -a v1.1 -m "Parse latest Revolut CSV export format"
    ```
2. Push commit and tags to github
   ```bash
    git push origin master --tags
    ```
3. Create a new release in [Github repo Releases](https://github.com/FnTm/ofxstatement-lv/releases/new)
4. Build new Docker images
   ```bash
    docker build --platform=amd64 -f Dockerfile -t fntm/ofxstatement-lv:v1.1 -t fntm/ofxstatement-lv:latest .
    ```
5. Log into Dockerhub
   ```bash
    docker login
    ```
6. Push latest tagged builds up to Dockerhub
   ```bash
    docker push fntm/ofxstatement-lv:latest
    ```