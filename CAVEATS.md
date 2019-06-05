# esdeploy

### Please be aware of the following issues:

 * For those configuring Metricbeat to monitor Kibana, the following patch should
 be applied to Kibana or you will receive 500 errors from the Kibana API:

 https://github.com/elastic/kibana/pull/36986

 * The bs1.prod image does not currently install Beats correctly. Please download
 and install Beats manually after bringing up the virtual machine. Downloads are
 available on elastic.co

