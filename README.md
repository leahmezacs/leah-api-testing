# Setup 
> I know it can be difficult, so stop me anytime if you have questions. These commands can be done on a mac or linux machine.

## Step 1: Git
> Open up your terminal to a desired directory for this project. 

Enter the following command, replacing leah with your name:

`mkdir leah-api-testing` [this creates a directory] 

Validate whether you have git installed:

`git --version` [if it returns nothing, you need to install git]

- If you dont have git installed:
  - [download git instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

- If you do have git installed, enter: 
  - `git clone https://github.com/leahmezacs/dredd-api-testing.git` [the readme.md will now download to your directory]

## Step 2: Node.js
> We will use a version manager to control the versions on node on our machines. 

1. Check if node and npm are already installed:
   
`node -v` [if it returns nothing, you need to install node - see #2]

`npm -v` [if it returns nothing, you need to install npm - see #3]

2. [Download NVM (Node Version Manager)](https://github.com/nvm-sh/nvm#git-install).

3. Use NVM to download version on node and npm:

`nvm install 12.20.1` [installs node version 12.20.1]

`nvm use 12.20.1` [node version for local directory]

`npm install -g npm` [install npm]

4. Config NPM project.   

The next command will prompt some questions:

`npm init` [interactive configuration]

Press enter for all questions. And lastly, enter yes to `Is this OK?`.

In the new file package.json, replace 
```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
with
```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": ""
  },
```

## Step 3: Dredd
> In the same directory, we will install dredd and configure framework.

#### Dredd Documentation: `https://www.npmjs.com/package/dredd/v/11.2.19`

`npm install -g dredd` [install [dredd]()]

`dredd --version` [check if it installed correctly]

Create a file named: `animal_crossing_apis.apib`

The next command will prompt some questions:

`dredd init` [interactive configuration]

1. ? Location of the API description document. Answer: `./animal_crossing_apis.apib`
2. ? Command to start the API server under test. Answer: `npm start`
3. ? Host of the API under test. Answer: leave blank!
4. ? Do you want to use hooks to customize Dredd's behavior? Answer: `n`
5. ? Do you want to report your tests to the Apiary inspector?. Answer: `n`
6. ? Dredd is best served with Continuous Integration. Do you want to create CI configuration? Answer: `n`

## Step 4: Example of a test.

Today we are using an api blueprint file to test our api against documentation. The apis we will be testing is free from `http://acnhapi.com`. Copy and paste the code below into your file animal_crossing_apis.apib.

>  API Blueprint documentation: `https://apiblueprint.org/`

```
FORMAT: 1A 
# Animal Crossings GET APIs 


## Get Existing Bug information [GET /v1/bugs/54]


+ Request
    + Headers

            content-type: application/x-www-form-urlencoded
       
+ Response 200
```

In order to link the configuration file (dredd.yml that was created by `dredd init`), to the documentation file (animal)crossing_apis.apib), we need to change a few lines:

- `blueprint: ./animal_crossing_apis.apib`
- `endpoint: 'http://acnhapi.com'`


## Step 4: Runnning Tests

Just run `dredd` to run the tests.
