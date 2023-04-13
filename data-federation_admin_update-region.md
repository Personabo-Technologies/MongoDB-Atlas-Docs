Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update a Federated Database Instance Region

Share Feedback

You can change the AWS region through which your federated database instance
requests are routed. By default, Data Federation requests are routed through
the region that is closest to your client application. The region that is
closest to your application may be different from the regions that house your
data stores.

## Note

If you change the AWS region through which your federated database instance
requests are routed, you must update your federated database instance
connection string with the new hostname. This change ensures that your
requests are routed through the new region.

## Procedure

To change the AWS region through which your federated database instance
requests are routed, do the following in the Atlas UI:

1

### Select Data Federation from the left-hand navigation.

2

### Click Ellipses (...) for your federated database instance.

3

### Select Update Region from the dropdown to display the Update Region modal.

4

### Choose the region through which to route your federated database instance
requests:

  * The closest available region to allow Atlas to automatically choose the Data Federation region closest to you.

  * A specific region to specify the region through which your federated database instance requests must be routed.

You can select from the following regions:

Data Federation Regions

|

AWS Regions  
  
|  
  
Virginia, USA

|

us-east-1  
  
Oregon, USA

|

us-west-2  
  
Sao Paulo, Brazil

|

sa-east-1  
  
Ireland

|

eu-west-1  
  
London, England

|

eu-west-2  
  
Frankfurt, Germany

|

eu-central-1  
  
Mumbai, India

|

ap-south-1  
  
Singapore

|

ap-southeast-1  
  
Sydney, Australia

|

ap-southeast-2  
  

5

### Click Save for the changes to take effect.

The federated database hostname in your current federated database instance
connection string will continue to work. However, to use the region you
selected, you must update the federated database hostname in your federated
database instance connection string. To utilize the new region, click the
Connect button for your federated database instance and follow the steps in
Connect to Your Federated Database Instance.

