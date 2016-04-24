# Instructions

1. Add jar file  “pg-checksum-1.0-jar-with-dependencies.jar” as a “Reference” in your project.
2. The above mentioned jar file contains methods for generating and validating Checksum. These methods are as given below and their respective usage is given in the next two points.
 ```sh
 String checkSumServiceHelper.genrateCheckSumGAE(String merchantKey,TreeMap reqMap);
 boolean  checkSumServiceHelper.verifycheckSumGAE (String merchantkey, TreeMap   responseTreeMap, String responseChecksum);
 ```
 
3. For Generating CheckSum, use the following snippet code:
 ```sh
 com.paytm.merchant.CheckSumServiceHelper checkSumServiceHelper = com.paytm.merchant.CheckSumServiceHelper.getCheckSumServiceHelper();
 
 TreeMap<String,String> parameters = new TreeMap<String,String>();
 String merchantKey = "xxxxxxxxxxxxxxxxx"; //Key provided by Paytm
 parameters.put("MID", "xxxxxxxxxxxxxxxxxxxxxx"); // Merchant ID (MID) provided by Paytm
 parameters.put("ORDER_ID", "nnnnnnnnn"); // Merchant’s order id
 parameters.put("CUST_ID", "CUST001"); // Customer ID registered with merchant
 parameters.put("TXN_AMOUNT", "1");
 parameters.put("CHANNEL_ID", "WEB");
 parameters.put("INDUSTRY_TYPE_ID", "Retail"); //Provided by Paytm
 parameters.put("WEBSITE", "xxxxxxxxxxx"); //Provided by Paytm
 //Note: Above mentioned parameters are not complete list of parameters. Please refer integration document for additional parameters which need to be passed.
 String checkSum = checkSumServiceHelper.genrateCheckSumGAE(merchantKey, parameters);
 ```
4. For Verifying CheckSum, use the following snippet code
 ```sh
 com.paytm.merchant.CheckSumServiceHelper checkSumServiceHelper = com.paytm.merchant.CheckSumServiceHelper.getCheckSumServiceHelper();
 
 TreeMap<String,String> parameters = new TreeMap<String,String>();
 String paytmChecksum = "xxxxxxxxxxxx"; // Sent by Paytm pg
 boolean isValidChecksum = false;
 
 paytmChecksum = request.getParameter("CHECKSUMHASH");
 
 String merchantKey = "xxxxxxxxxxxxxxxxx"; //Key provided by Paytm
 parameters.put("MID", "xxxxxxxxxxxxxxxxxxxxxx"); // Merchant ID (MID) sent by Paytm pg
 parameters.put("TXNID", ""); // Transaction id sent by Paytm pg
 parameters.put("ORDER_ID", "nnnnnnnnn"); // Merchant’s order id
 parameters.put("BANKTXNID", "xxxxxxxxxxxx");  // Bank TXN id sent by Paytm pg
 parameters.put("TXN_AMOUNT", "1");
 parameters.put("STATUS", " TXN_FAILURE"); //sent by Paytm pg
 parameters.put("RESPCODE", "xxxxxxxxxxx"); //sent by Paytm pg
 //Note: Above mentioned parameters are not complete list of parameters. Please refer integration document for additional parameters which need to be passed.
 isValidChecksum = checkSumServiceHelper.verifycheckSumGAE (merchantkey, parameters, paytmChecksum);
 ```
5. Integration Doc is [here](http://paywithpaytm.com/developer/paytm_api_doc/)
