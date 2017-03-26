# Transform statements from Latvian banks to OFX using Docker

If you're using a financial tool like [YNAB](https://http://www.youneedabudget.com/) you know that entering all of your transactions can be a pain. And even though tools like YNAB offer importing transactions directly from your bank, unless you're in US you're probably out of luck.

YNAB allows you to import OFX files which can make this process easier. [OFX Statement](https://github.com/kedder/ofxstatement) is a project that provides a plugin-enabled architecture, where anyone can create a compatible plugin for their local banks.

This project is made possible by [Gints Murāns' OFX parsers for Latvian banks](https://github.com/gintsmurans/ofxstatement-latvian). Major kudos!

## Usage
 ```
 docker run -v ~/dev/ofx/data:/data fntm/ofxstatement-lv ofxstatement convert -t swedbankLV /data/statement.csv /data/swed.ofx
 ```
The example above assumes that
- You have a folder named data which can be linked as volume to the docker container (needed to give ofxstatement access to that file)
- You have downloaded a .csv statement from Latvian swedbank in said folder
