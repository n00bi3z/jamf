# jamf
Random jamf scripts I create. More details as I create scripts

I basically did some elementary wizardry to get what I wanted

So far through jamf api, the python script:

1. Uses jamf creds to request a token
2. From user input, searches serial number
3. From the returned xml value of serial number, the device id in jamf is stripped
4. Searches the json for the "extensionAttributes" details (type(dict))
5. Makes a somewhat pretty output using an f-string
