---
layout: post
title:  "Flashboard Introduction"
date:   2017-07-03 15:20:12
categories: Startup
---

# Flashboard Introduction

## flashboard can handle your whole back-end includes services, rest-full api and admin dashboard based on loopback node.js framework. 

***Simply can define your models with several options and get your rest-full api and admin dashboard automatically.***


https://d2mxuefqeaa7sj.cloudfront.net/s_39D514CB13606B2A57CDEE42F601CC2243937ECA3F60FB1607EFC679C19DC7BC_1499086353020_demo.jpg


Admin dashboard implemented by [vue.js 2 framework](https://vuejs.org/) and [muse-ui](http://www.muse-ui.org/) as ui-component library that allows you have a multiple themes for your user interface.
You have a database-connector options that allows you to connect your back-end to each database you want such as mongodb or mysql and etc.

Let’s start to build your own back-end services.


## Installation
1. Before you begin, make sure you have [Node.js](http://nodejs.org/download) and [MongoDB](http://www.mongodb.org/downloads) installed. For best results, use the latest LTS (long-term support) release of Node.js.
2. Running below command in your empty project directory path :
    $ git clone https://github.com/vah7id/flashboard.git
3. First install your services packages by run below command on your project directory :
    $ npm run preinstall
4. Install your admin generator packages by run below command on root directory:
    $ npm install
5. Running back-end services first before running admin dashboard :
    $ npm run service
6. At last you can run your admin dashboard by running below command:
    $ npm run dev

for deploy on production you can run build command :

    $ npm run build



# Models

In this part we can learn how to create own models and start to build your back-end project. there are several options to create your models and modify them.
According to [loopback model definition](http://loopback.io/doc/en/lb3/Defining-models.html) rules:

> A LoopBack model is a JavaScript object with both Node and REST APIs that represents data in backend systems such as databases. Models are connected to backend systems via data sources. You use the model APIs to interact with the data source to which it is attached.
> Additionally, you can add functionality such as validation rules and business logic to models.
> Every LoopBack application has a set of predefined [built-in models](http://loopback.io/doc/en/lb3/Using-built-in-models.html) such as User, Role, and Application. You can [extend built-in models](http://loopback.io/doc/en/lb3/Extending-built-in-models.html) to suit your application’s needs.
> Additionally, you can [define your own custom models](http://loopback.io/doc/en/lb3/Creating-models.html) specific to your application. You can create LoopBack models several different ways:
1. With the command-line tool, by using the LoopBack model generator.
2. From an existing relational database, by using model discovery.
3. From free-form data in NoSQL databases or REST APIs by using instance introspection.
> These methods all create a [Model definition JSON file](http://loopback.io/doc/en/lb3/Model-definition-JSON-file.html) that defines your model in LoopBack.
> You can also create and customize models programmatically using the [LoopBack API](http://apidocs.strongloop.com/loopback/#loopback-createmodel), or by manually editing the [model definition JSON file](http://loopback.io/doc/en/lb3/Model-definition-JSON-file.html).
> In most cases, you shouldn’t need to use those techniques to create models, but you generally will use them to modify and customize models.
> Once you’ve created a model, you can [customize it](http://loopback.io/doc/en/lb3/Customizing-models.html) to suit your needs, and also add [data validation](http://loopback.io/doc/en/lb3/Validating-model-data.html) and create [relationships among models](http://localhost:4001/doc/en/lb3/Creating-model-relations.html).
> Models come with a standard set of REST endpoints for create, read, update, and delete (CRUD) operations on model data. You can customize a model’s endpoints; see [Exposing models over REST](http://loopback.io/doc/en/lb3/Exposing-models-over-REST.html).


## Create Model
1. Using the model generator :
2. The easiest way to create a new model is with the [model generator](http://loopback.io/doc/en/lb3/Model-generator.html).
3. just run below command on projectDirectory/api


    $ lb model <modelName>

When creating a new model, the generator will prompt you for the properties in the model. Subsequently, you can add more properties to it using the [property generator](http://loopback.io/doc/en/lb3/Property-generator.html).
When you create a model (for example, called “myModel”), the tool:


- Creates `**/api/common/models/myModel.json**`, the [model definition JSON file](http://loopback.io/doc/en/lb3/Model-definition-JSON-file.html).
- Creates `**/api/common/models/myModel.js**`, where you can extend the model programmatically. For example to add remote methods. See [Adding application logic](http://loopback.io/doc/en/lb3/Adding-application-logic.html) for more information.
- Adds an entry to `**/api/server/model-config.json**` for the model, specifying the model’s data source. See [model-config.json](http://loopback.io/doc/en/lb3/model-config.json.html) for more information.

After you create a model, you can add more properties with the [property generator](http://loopback.io/doc/en/lb3/Property-generator.html).


    $ lb property

The tool will prompt you to choose the model to which you want to add the property, along with the other property settings (as before). Then, it will modify the [model definition JSON file](http://loopback.io/doc/en/lb3/Model-definition-JSON-file.html) accordingly.


2. **Using the model json file**

LoopBack *adds* the settings in the the model JSON file to those of the base model. follow the below steps to create your manual model.

Adds an entry to `**/api/server/model-config.json**` for the model, specifying the model’s data source. append your model as json item end of this file like below:


      "myModel": {
        "dataSource": "myDb",
        "public": true
      }

dataSource: Name of the data source to which the model is connected. Must correspond to a data source defined in [datasources.json](http://loopback.io/doc/en/lb3/datasources.json.html).
public: Whether the model API is exposed. If true, then the model is exposed over REST. Does not affect accessibility of Node API.

Creates `**/api/common/models/myModel.json**`, the [model definition JSON file](http://loopback.io/doc/en/lb3/Model-definition-JSON-file.html).


    {
      "name": "myModel",
      "base": "PersistedModel",
      "strict": false,
      "idInjection": false,
      "options": {
        "validateUpsert": true
      },
      "properties": {
        "id": {
          "type": "string",
          "id": true,
          "index": true
        },
        "propertyName": {
          "type": "string",
          "required": true
        }
      },
      "validations": [],
      "relations": {},
      "acls": [],
      "methods": {}
    }

Creates `**/api/common/models/myModel.js**`, where you can extend the model programmatically.


    'use strict';
    module.exports = function(myModel) {
    
    };

After create your models you should restart your server script by run npm run service.
In Model Config ( next section ) you can reach to the information about how to set properties, options, validations, relations and methods.


> In general, use `**PersistedModel**` as the base model when you want to store your data in a database using a connector such as MySQL or MongoDB. Use `**Model**` as the base for models that don’t have CRUD semantics, for example, using connectors such as SOAP and REST.

For example, here is an excerpt from a `**customer.json**` file that extends the built-in User model to define a new Customer model:


    {
      "name": "Customer",
      "base": "User",
      "idInjection": false,
    ...

In general, you can extend any model this way, not just the built-in models.


> Important:
> Currently you cannot modify a built-in model’s required properties. If you need to do this, then create your own custom model as a replacement instead.

You can checkout the documentation models part and get more information about models configs, options, validation and etc.

https://vah7id.github.io/flashboard/models.html

Flashboard create a admin dashboard based on configuration of loopback models. there are several settings and options on your models and user interface generation types and formats. 


## Datasource Config
https://d2mxuefqeaa7sj.cloudfront.net/s_C6F5F8DD00AAA5BB7C357F785D033530B83284EC7F641341E97DA691D97B8750_1496961366393_9830484.png


LoopBack models connect to backend systems such as databases via *data sources* that provide create, retrieve, update, and delete (CRUD) functions. LoopBack also generalizes other backend services, such as REST APIs, SOAP web services, and storage services, and so on, as data sources.
Data sources are backed by *connectors* that implement the data exchange logic using database drivers or other client APIs. In general, applications don’t use connectors directly, rather they go through data sources using the [DataSource](http://apidocs.strongloop.com/loopback-datasource-juggler/#datasource-new-datasourcename-settings) and [PersistedModel](http://apidocs.strongloop.com/loopback/#persistedmodel-new-persistedmodel) APIs.
Basic procedure
To connect a model to a data source, follow these steps:


1. Use the [data source generator](https://loopback.io/doc/en/lb2/Data-source-generator.html) to create a new data source.
    $ slc loopback:datasource ? Enter the data-source name: mysql-corp ? Select the connector for mysql: MySQL (supported by StrongLoop)

Follow the prompts to name the datasource and select the connector to use. This adds the new data source to `**[datasources.json]**`
`**(https://loopback.io/doc/en/lb2/datasources.json.html)**`.


2. Edit `**api/server/datasources.json**` to add the necessary authentication credentials: typically hostname, username, password, and database name.

For example:
api/server/datasources.json


    "mysql-corp": { "name": "mysql-corp", "connector": "mysql", "host": "your-mysql-server.foo.com", "user": "db-username", "password": "db-password", "database": "your-db-name" }

For information on the properties that each connector supports, see documentation for the specific connector under [Connectors reference](https://loopback.io/doc/en/lb2/Connectors-reference).

3. Install the corresponding connector as a dependency of your app with `**npm**`.

For example:

    $ cd <your-app>/api $ npm install --save loopback-connector-mysql

See [Connectors reference](https://loopback.io/doc/en/lb2/Connectors-reference). for the list of connectors.

1. Use the [model generator](https://loopback.io/doc/en/lb2/Using-the-model-generator.html) to create a model.


    $ slc loopback:model ? Enter the model name: myModel ? Select the data-source to attach myModel to: mysql (mysql) ? Select model's base class: PersistedModel ? Expose myModel via the REST API? Yes ? Custom plural form (used to build REST URL): Let's add some test2 properties now. ...

When prompted for the data source to attach to, select the one you just created.
Note: The model generator lists the [memory connector](https://loopback.io/doc/en/lb2/Memory-connector.html), “no data source,” and data sources listed in `**[datasources.json](https://loopback.io/doc/en/lb2/datasources.json.html)**`. That’s why you created the data source first in step 1.

You can also create models from an existing database; see [Creating models](https://loopback.io/doc/en/lb2/Creating-models.html) for more information.


# Rest-full API

Once you have defined a model, then you can use create, read, update, and delete (CRUD) operations to add data to the model, manipulate the data, and query it. All LoopBack models that are connected to persistent data stores (such as a database) automatically have the create, retrieve, update, and delete operations of the [PersistedModel](http://apidocs.strongloop.com/loopback/#persistedmodel-new-persistedmodel) class.

| Operation          | REST                                                                                                                                                                                                                                                                                                                                                                                       | LoopBack model method (Node API)* | Corresponding SQL Operation |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------- | --------------------------- |
| Create             | [PUT /](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#create-model-instance)[*modelName*](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#create-model-instance)
[POST /](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#update--insert-instance)[*modelName*](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#update--insert-instance) | create()*                         | INSERT                      |
| | Read (Retrieve)  | [GET /modelName?filter=…](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#find-matching-instances)                                                                                                                                                                                                                                                                             | find()*                           | SELECT                      |
| | Update (Modify)  | [POST /](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#update--insert-instance)[*modelName*](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#update--insert-instance)
[PUT /modelName](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#update-model-instance-attributes)                                                                             | updateAll()*                      | UPDATE                      |
| | Delete (Destroy) | [DELETE /](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#delete-model-instance)[*modelName*](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#delete-model-instance)[/](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#delete-model-instance)[*modelID*](https://loopback.io/doc/en/lb2/PersistedModel-REST-API.html#delete-model-instance)          | destroyById()*                    | DELETE                      |

(*) Methods listed are just prominent examples; other methods may provide similar functionality; for example: `**findById()**`, `**findOne()**`, and `**findOrCreate()**`. See [PersistedModel API documentation](http://apidocs.strongloop.com/loopback/#persistedmodel) for more information.


## Create Simple API

first we are going to create a CoffeeShop model that will automatically have REST API endpoints.
Go into your new application directory, then run the LoopBack model generator:


    $ cd api
    $ slc loopback:model

The generator will prompt for a model name. Enter CoffeeShop:

    [?] Enter the model name: CoffeeShop

It will ask if you want to attach the model to any data sources that have already been defined.
At this point, only the default in-memory data source is available. Press Enter to select it:


    ...
    [?] Select the data-source to attach CoffeeShop to: (Use arrow keys)
    ❯ db (memory)

Then the generator will prompt you for the base class to use for the model. Since you will eventually connect this model to a persistent data source in a database, press down-arrow to choose PersistedModel, then press Enter:


    [?] Select model's base class: (Use arrow keys)
      Model
    ❯ PersistedModel
      ACL
      AccessToken
      Application
      Change
      Checkpoint

PersistedModel is the base object for all models connected to a persistent data source such as a database. See LoopBack core concepts for an overview of the model inheritance hierarchy.
One of the powerful advantages of LoopBack is that it automatically generates a REST API for your model. The generator will ask whether you want to expose this REST API.
Hit Enter again to accept the default and expose the Person model via REST:


    [?] Expose CoffeeShop via the REST API? (Y/n) Y

LoopBack automatically creates a REST route associated with your model using the plural of the model name. By default, it pluralizes the name for you (by adding “s”), but you can specify a custom plural form if you wish. See Exposing models over REST for all the details.
Press Enter to accept the default plural form (CoffeeShops):


    [?] Custom plural form (used to build REST URL):

Next, you’ll be asked whether you want to create the model on the server only or in the `**/common**`directory, where it can potentially be used by both server and client LoopBack APIs. Keep, the default, common, even though in this application you’ll only be working with server-side models:


    ? Common model or server only? ❯ common server

Every model has properties. Right now, you’re going to define one property, “name,” for the CoffeeShop model.
Select `**string**` as the property type (press Enter, since string is the default choice):


    Let's add some CoffeeShop properties now.
    Enter an empty property name when done.
    [?] Property name: name
       invoke   loopback:property
    [?] Property type: (Use arrow keys)
    ❯ string
      number
      boolean
      object
      array
      date
      buffer
      geopoint
      (other)

Each property can be optional or required. Enter `**y**` to make `**name**` required:

    [?] Required? (y/N)

Then you’ll be prompted to enter a default value for the property; press Enter for no default value:

    ? Default value[leave blank for none]:

Then, you’ll be prompted to add another property. Follow the prompts to add a required property named “city.”

    Let's add another CoffeeShop property.
    ? Property name: city
    ? Property type: string
    ? Required? Yes
    ? Default value[leave blank for none]:

End the model creation process by pressing Enter when prompted for the name of the next property.
The model generator will create two files in the application’s `**common/models**` directory that define the model: `**coffee-shop.json**` and `**coffee-shop.js**`.


> Important: The LoopBack model generator, automatically converts camel-case model names (for example MyModel) to lowercase dashed names (my-model). For example, if you create a model named “FooBar” with the model generator, it creates files `**foo-bar.json**`and `**foo-bar.js**` in `**common/models**`. However, the model name (“FooBar”) will be preserved via the model’s name property.

Check out the project structure:
For all the details of the canonical LoopBack application structure, see Project layout reference.
First, start the application:


    $ npm run service
    ...
    Browse your REST API at http://0.0.0.0:3000/explorer
    Web server listening at: http://0.0.0.0:3000/

Note: Running your app with the `**node**` command is appropriate when you’re developing on your local machine. In production, consider using API Connect or a process manager for scalability and reliability.
Open your browser to [http://0.0.0.0:3000/](http://0.0.0.0:3000/) (on some systems, you may need to use [http://localhost:3000](http://localhost:3000/) instead). You’ll see the default application response that displays some JSON with some status information; for example:

    {"started":"2017-03-10T21:59:47.155Z","uptime":42.054}

Now open your browser to [http://0.0.0.0:3000/explorer](http://0.0.0.0:3000/explorer) or [http://localhost:3000/explorer](http://localhost:3000/explorer). You’ll see the StrongLoop API Explorer:

https://loopback.io/images/5570638.png


Through a set of simple steps using LoopBack, you’ve created a CoffeeShop model, specified its properties and then exposed it through REST.


## API Explorer

You’re not the only one who’ll use the API you just created. That means you’ll need to document your API. Fortunately, LoopBack provides API Explorer for you.

**Run API Explorer**
Note: API Designer Explorer’s functionality is the same as StrongLoop Explorer. The instructions and screenshots below are for the StrongLoop tools.
Run the application:

    `$ npm run service

Now go to [http://localhost:3000/explorer](http://localhost:3000/explorer). You’ll see the StrongLoop API Explorer showing the two models this application has: Users and CoffeeShops:

https://loopback.io/images/5570639.png

## Contribute

Contributions welcome! Like seriously
If you have a any issue with flashboard feel free to [report it in github](https://github.com/vah7id/flashboard/issues)
We need to improve the admin dashboard with more options and features. 
Next step is creating the GUI for creating and managing models and API's. 

