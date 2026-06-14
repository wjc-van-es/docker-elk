<style>
body {
  font-family: "Spectral", "Gentium Basic", Cardo , "Linux Libertine o", "Palatino Linotype", Cambria, serif;
  font-size: 100% !important;
  padding-right: 12%;
}
code {
  padding: 0.25em;
	
  white-space: pre;
  font-family: "Tlwg mono", Consolas, "Liberation Mono", Menlo, Courier, monospace;
	
  background-color: #ECFFFA;
  //border: 1px solid #ccc;
  //border-radius: 3px;
}

kbd {
  display: inline-block;
  padding: 3px 5px;
  font-family: "Tlwg mono", Consolas, "Liberation Mono", Menlo, Courier, monospace;
  line-height: 10px;
  color: #555;
  vertical-align: middle;
  background-color: #ECFFFA;
  border: solid 1px #ccc;
  border-bottom-color: #bbb;
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 #bbb;
}

h1,h2,h3,h4,h5 {
  color: #269B7D; 
  font-family: "fira sans", "Latin Modern Sans", Calibri, "Trebuchet MS", sans-serif;
}

</style>

# Tutorial #04 - Collecting logs with Filebeat

## Context
- _Filebeat_ is a service that can monitor logfiles to ingest their logs into _ElasticSearch_.
- We can install & configure it on our laptop and point it to some of our application log files like

  <a href="file:///home/willem/application-logs/full-text-search/full-text-search-application.log">full-text-search-application.log</a>

- Use 
  [https://www.elastic.co/docs/reference/beats/filebeat/filebeat-installation-configuration](https://www.elastic.co/docs/reference/beats/filebeat/filebeat-installation-configuration)
  for installation and configuration hints
- See
  [https://www.elastic.co/docs/reference/beats/filebeat/running-with-systemd](https://www.elastic.co/docs/reference/beats/filebeat/running-with-systemd)
  to see details about _systemd_ service configuration.

## Installation
