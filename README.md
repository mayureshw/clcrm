# clcrm - command line crm tool using vim outliner

## Features

1. Maintaining history of interactions

    - Register `parties` with whom you have interactions. Parties can be of various
      types, depending on the activity you are using the crm for. A party can be an
      individual, group, business entity - whatever you want to maintain record of
      interactions with.
    
    - Record discussions in otl form. The otl file is identified by the
      registration number of the party and the date of the discussion.
    
    - View history of interactions with a given party in reverse chronological
      order.

1. System of records and generation of PDFs from filled forms, on your letterhead

    - You can configure your own forms in otl form.
    
    - You can write a converter for these forms into PDFs using latex and
      [pyexpander](https://pyexpander.sourceforge.io/) tool. The filled form and
      the registration information of hte party for which it is filled are made
      available as python objects to the latex macro file.
    
    - Keyboard shortcuts to generate a PDF from the form, share the PDF over email
      or whatsapp, with some additional setup.

1. Financial management

    - WIP

## Installation

1. Clone this repository in a suitable directory. For convenience of
   documentation let us assume that you install in directory `$HOME/programs`.

    ```
    git clone --depth 1 https://github.com/mayureshw/clcrm $HOME/programs
    ```

1. You need to choose two directories to store your configuration database and
   crm database and set their paths in your environment. E.g. if you are using
   bash shell, you may add these to your $HOME/.bashrc file and reopen the
   session for the environment changes to take effect.

    ```
    export CRM_CONFDIR=$HOME/crmconfdb
    export CRM_DBDIR=$HOME/crmdb
    source $HOME/programs/clcrm/bin/crmrc
    ```

1. You need to configure your installation as described in the next section.

   It is advisable that whatver contents you create in $CRM_CONFDIR, you keep
   them in some revision control system such as git.

   Contents of $CRM_DBDIR are kept under revision control by clcrm. But you
   should ensure that its backup is maintained on a different disk for safety.


## Configuration

1. See examples/crmconfdb folder for a sample configuration.

1. You need to add your forms in $CRM_CONFDIR/vimforms.

   To start using the system at least one form is mandatory with name
   `registration` in which you capture the fields, such as name, type etc.  of
   a party you want to register.

   A form is identified by the following files:

    - \<formname\>.otl : Simply an otl file that will appear in your meeting
      record as-is. This is a template, a document tree. At leaf level of this,
      data values will be recorded when filling the form.

    - \<formname\>.help : A text file in which you can write help to fill this
      form.

1. Only the `top level` forms can be invoked for populating. Top form fields
   appear at indent level 1. But there may be `sub forms` a higher level form
   may refer to, which will have their contents at their invocation's level+1

1. If you want some forms to choose from a drop down, you can record the drop
   down contents in a sub-form.

1. vimforms directory should contain (at least a blank) metadata.otl file.
   This file is used to mark the fields that may accept multiple values and
   fields (lists of elementary data values) and structures that may accept
   multiple values (lists of structures). (TODO: Will add an example.)

1. If you want to generate PDF files from filled forms you have to define a
   corresponding latex template using the
   [pyexpander](https://pyexpander.sourceforge.io/) syntax. A Python object
   corresponding to the filled form and the registration object of the party
   against which the form is recorded are made available to the template.
   (TODO: Will add an example.)

## Usage

Command `crm_help` should give the usage information of various commands.

You will almost always begin with `crm_register` command, of course after you
have created your registration form as described in the previous section.

## Wish list

This tool is primarily for those who like the power of command line tools and
the vim editor. It is possible to extend it to more users by building other
types of UI, such as web UI. I may add a web UI to this tool in future.
