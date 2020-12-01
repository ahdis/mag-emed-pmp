##  adapt the keystore for another endpoint

### add new certificate
openssl s_client -showcerts -connect sct-form.hcuge.ch:443
openssl s_client -connect sct-form.hcuge.ch:443 | openssl x509 -out sct-form.hcuge.cert

270.jks, defuault keystore gazelle, copy to hcuge.jks
keytool -import -alias hcuge_cer -file sct-form.hcuge.cert -keystore hcuge.jks
