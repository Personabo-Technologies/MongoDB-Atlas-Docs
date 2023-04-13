Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage the Atlas CLI

Share Feedback

On this page

  * Generate an Autocompletion Script
  * Create and Manage Atlas CLI Profiles
  * Configure an Atlas CLI Profile
  * Update a Profile in the Terminal
  * Update a Profile in a Text Editor
  * View a Profile
  * Rename a Profile
  * Delete a Profile

Use the following resources to manage the Atlas CLI itself.

## Note

Before you run any Atlas CLI commands, you must:

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Generate an Autocompletion Script

Bash

fish

PowerShell

zsh

To learn how to generate the autocompletion script for Bash, see atlas
completion bash.

## Create and Manage Atlas CLI Profiles

Use the following resources to create and manage profiles.

For step-by-step instructions on saving connection settings as profiles, see
Save Connection Settings.

### Configure an Atlas CLI Profile

To set up an Atlas CLI profile using the Atlas CLI, run the following command:

    
    
    atlas config init [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas config init.

### Update a Profile in the Terminal

To update values in an Atlas CLI profile using the Atlas CLI, run the
following command:

    
    
    atlas config set <propertyName> <value> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas config set.

### Update a Profile in a Text Editor

To open the config file for your Atlas CLI profile with the default text
editor using the Atlas CLI, run the following command:

    
    
    atlas config edit [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas config edit.

### View a Profile

To return the details of the Atlas CLI profile you specify using the Atlas
CLI, run the following command:

    
    
    atlas config describe <name> [options]  
      
  
To list all Atlas CLI profiles using the Atlas CLI, run the following command:

    
    
    atlas config list [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas config describe and atlas config list.

### Rename a Profile

To rename an Atlas CLI profile using the Atlas CLI, run the following command:

    
    
    atlas config rename <oldProfileName> <newProfileName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas config rename.

### Delete a Profile

To delete an Atlas CLI profile using the Atlas CLI, run the following command:

    
    
    atlas config delete <name> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas config delete.

← Atlas CLIReference →

