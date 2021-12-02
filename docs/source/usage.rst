Usage
=====

.. _installation:

Configuration
------------

Configuration on ELI takes places within a single Excel Spreadsheet. This Spreadsheet must be stored on OneDrive Business, or within Sharepoint. The Excel Spreadsheet contains the following information:

1. User Names, Credentials, Email Addresses and Team Information
2. Laboratory Computer Configuration
3. Complete Experiment Information

User information is configured within the User table in the Config worksheet. You must specify a name, an email address, a password (autogenerate using RAND in excel) and an group number. Students within the same group will be assigned to the same plant and lab computer. Additionally, Students within the same group will have their web views synchronised to enable collaboration

Experiment Information is contained within Spreadsheets, whose names correspond to the experiments. Experiments ought be organised so that one experiment corresponds to one laboratory experiment. Experiment Information contains a ComponentX table and a SectionX Table (X corresponds to some number, since tables can't have the same name in excel even if they are on different worksheets). The ComponentX table contains all components that students can access for the entire laboratory experiment. This should contain "extra" resistors and capacitors, just as an in-person laboratory would, in order to make design sufficiently challenging. The Name must correspond to the component name in the SPICE model. The Type must correspond to an entry in the Component JSON (see below). Values must correspond to the SPICE model for the same component name (i.e. if R1 in SPICE is 1kOhm, R1 must be 1k in the Table)

Component Configuration takes place within the ELI Webserver (see below). To Add Components, you must add a JSON object to the end of the component array stored in the component JSON file available at the root of the webserver. An example component configuration is below. The component must contain both a "model" and "physical" object, which corresponds to the circuit model representation and breadboard representation respectively. Each object must contain a reference to an "image" stored in the Webserver. The Connector object specifies the relative location of the connectors with respect to the image (you may need to experiment with these locations)

  "resistor":{
    "model":{
    "image":"img/res.png",
    "connectors": {
      "1":{
        "top":-3,
        "left":0
      },
      "2":{
        "top":-3,
        "left":80
      }
    },
    "label":{
      "top":-20,
      "left":17,
      "default":"1k"
    }
    },
    "physical":{
    "image":"img/resistor-physical.svg",
    "connectors": {
      "1":{
        "top":-3,
        "left":0
      },
      "2":{
        "top":-3,
        "left":80
      }
    },
    "label":{
      "top":-20,
      "left":17,
      "default":"1k"
    }
    }
  },

Web Server Installation
------------

Note

Installation of the ELI Web Server requires technical knowledge and access to cloud services (Microsoft Azure, Heroku, etc).

You will need access to the ELI Node.JS Source Code. You can implement this via Visual Studio to a Microsoft Azure App Service, or to Heroku or Similar. It is also possible (but not recommended) to install the ELI Application on a local web server. You will need to configure Environment Variables. 

Administering ELI
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

