Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# External Dependencies

Share Feedback

On this page

  * Overview
  * Upload External Dependencies
  * Procedure
  * Import External Dependencies
  * Usage
  * Import a Full Module
  * Import a Module Subfolder
  * Constraints

## Overview

An external dependency is an external library that includes logic you'd rather
not implement yourself, such as string parsing, convenience functions for
array manipulations, and data structure or algorithm implementations.

You can upload external dependencies from the npm repository to App Services
and then import those libraries into your functions using standard JavaScript
module syntax. To get started with external dependencies, check out the
following guides.

## Note

### Create Your Own Modules

Though most npm modules are written by third parties, you can create and
publish your own npm modules to house logic specific to your application. You
can make your modules available to the Node.js community or reserve them for
private use. To learn more, see npm's guide on Contributing packages to the
registry.

## Upload External Dependencies

You can upload npm modules into the App Services application that houses your
triggers and functions. This allows functions in your application to depend
upon external libraries.

To use external dependencies, upload an archive of an npm `node_modules`
folder via the App Services UI. Once uploaded, any function can import and use
any dependencies listed on the dependencies page of the App Services UI.

## Important

### External Dependency Size Constraints

Uploaded zip files are subject to a `10MB` size cap.

### Procedure

1

#### Install your dependencies locally.

To upload external dependencies to Atlas App Services, you first need a local
`node_modules` folder containing at least one Node.js package. You can use the
following code snippet to locally install a dependency you would like to
upload:

    
    
    npm install <package name>  
      
  
If the `node_modules` folder does not already exist, this command
automatically creates it.

## Note

### Alternative Methods of Installation

You can also configure a `package.json` and run the `npm install` command to
install all packages (and their dependencies) listed in your `package.json`.

To learn more about npm and `node_modules`, consult the npm documentation .

2

#### Create a dependency archive.

Now that you've downloaded all of your npm modules, you need to package them
up in an archive so you can upload them to App Services. Create an archive
containing the `node_modules` folder:

    
    
    tar -czf node_modules.tar.gz node_modules/  
      
  
## Note

### Supported Archive Formats

App Services supports `.tar`, `.tar.gz`, and `.zip` archive formats.

3

#### Upload the dependency archive.

Once you've created an archive containing your dependencies, all that's left
to do is upload them to App Services. You can upload your dependency archive
using the App Services UI:

  1. Select App Services from the left-side navigation.

  2. Select the Triggers app.

## Note

Triggers created between 09 June 2020 and 01 June 2022 use the name
Triggers_RealmApp. Triggers created prior to 09 June 2020 use the name
Triggers_StitchApp.

  3. Select Functions from the left-side navigation.

  4. Select the Dependencies tab.

  5. Click the Upload Folder button.

  6. In the file picker, select the `node_modules.tar.gz` archive you just created and click Open. App Services automatically uploads the archive file, which may take several minutes depending on the speed of your internet connection and the size of your dependency archive. Whether the operation succeeded or failed, App Services displays a banner indicating the success or failure of the operation. If successful, the Dependencies tab displays a list of the dependencies that you included in your dependency archive.

  7. If drafts are enabled, you will also need to click Review & Deploy in the banner to apply these changes. If drafts are disabled, the change will take effect within 5 to 60 seconds.

Now that your dependencies have been uploaded, try importing them into a
Function.

## Import External Dependencies

Once uploaded to your application, you can import npm modules listed on the
dependencies page of the App Services UI into your functions.

## Note

### Pre-requisites for Import

You must upload dependencies before you can import them.

### Usage

You can import dependencies into any function using the `require` keyword
inside of the `exports` function. You cannot use ES Module `import` syntax.
You should import dependencies in the style of a `node_modules` module import,
since App Services does not support file or local module import. To learn more
about `require` syntax, consult the Node.js documentation for the require
keyword.

## Important

### Where Do I Import Modules?

Node.js projects commonly place `require` statements in the global scope of
each file, but App Services does not support this pattern. You _must_ place
function `require` statements within a function scope.

### Import a Full Module

Below, you'll find a simple example of a function that uses the `require`
keyword inside a function to import the `ramda` module and call ramda's `map`
method:

    
    
    exports = () => {  
      
       const R = require("ramda");  
       return R.map(x => x*2, [1,2,3]);  
    }  
  
### Import a Module Subfolder

The following example demonstrates how to use `require` to import a single
submodule of an external dependency into a function:

    
    
    exports = function(arg){  
      
       const cloneDeep = require("lodash/cloneDeep");  
      
       var original = { name: "Deep" };  
       var copy = cloneDeep(original);  
       copy.name = "John";  
      
       console.log(`original: ${original.name}`);  
       console.log(`copy: ${copy.name}`);  
       return (original != copy);  
    };  
  
## Constraints

External dependencies are subject to the following limitations:

  * Require statements _must_ appear inside a function declaration, not outside it. Atlas App Services does not currently support statements in the global scope.

  * Atlas App Services currently supports a subset of Node.js built-in modules. For a list of supported and unsupported modules, see function constraints.

← CRON ExpressionsSet Up and Query Data Federation →

