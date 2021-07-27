##  adapt the keystore for another endpoint

### add new certificate
openssl s_client -showcerts -connect sct-form.hcuge.ch:443
openssl s_client -connect sct-form.hcuge.ch:443 | openssl x509 -out sct-form.hcuge.cert

270.jks, defuault keystore gazelle, copy to hcuge.jks
keytool -import -alias hcuge_cer -file sct-form.hcuge.cert -keystore hcuge.jks


keytool -importkeystore -srckeystore /Users/oliveregger/Documents/github/k8s-fhir.ch/configurations/mag-test-chuv/client.p12 -destkeystore hcuge_cara.jks -srcstoretype pkcs12

keytool -import -alias adhis_cer -file /Users/oliveregger/Documents/github/k8s-fhir.ch/configurations/mag-test-chuv/ca.cer -keystore hcuge_cara.jks

