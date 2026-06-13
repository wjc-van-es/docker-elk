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

# Setup

## Context
- This repo is forked from
  [https://github.com/stacktrekker/docker-elk](https://github.com/stacktrekker/docker-elk)
- This repo provides the setup to follow a tutorial series on YouTube see playlist:
  [https://www.youtube.com/watch?v=Xff3dBZfPTk&list=PLApq3NZNbtW4v4qtTJR1-F4uFA5eXMTNl](https://www.youtube.com/watch?v=Xff3dBZfPTk&list=PLApq3NZNbtW4v4qtTJR1-F4uFA5eXMTNl)
- From the official Elastic site I will change the versions to the latest available ones:
  - `9.4.2` is an overall image version for elastic search, Kibana
     see info at
    - [https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-elasticsearch-docker-compose](https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-elasticsearch-docker-compose)
    - [https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-kibana-with-docker](https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-kibana-with-docker)

## Steps
1. Change `ELASTIC_VERSION=9.4.2` in [../.env](../.env)
2. Run `~/git/docker-elk$ docker compose up setup` to execute the one time setup service
   1. All created artifacts:
      ```bash
      ✔ Image docker-elk-elasticsearch       Built                                                                                                                                 70.3s
      ✔ Image docker-elk-setup               Built                                                                                                                                 70.3s
      ✔ Network docker-elk_elk               Created                                                                                                                                0.0s
      ✔ Volume docker-elk_elasticsearch      Created                                                                                                                                0.0s
      ✔ Container docker-elk-elasticsearch-1 Created                                                                                                                                0.4s
      ✔ Container docker-elk-setup-1         Created    
      ```
   2. These kept a running after the setup service completed
      1. `Container docker-elk-elasticsearch-1` and
      2. `Network docker-elk_elk`
   3. So we ran `~/git/docker-elk$ docker compose down` to quit them
3. We furthermore investigated
   1. image and volume with 
      1. `docker image ls`
      2. `~/git/docker-elk$ docker image inspect docker-elk-elasticsearch:latest > docker-elk-elasticsearch:latest:info.json`
      3. `~/git/docker-elk$ docker volume inspect docker-elk_elasticsearch > volume_docker-elk_elasticsearch.json`
4. Now we started docker compose `~/git/docker-elk$ docker compose up -d` to run the regular services, which are
   1. `elasticsearch`
   2. `logstash`, whose image still needed to be pulled on the first execution
   3. `kibana`
5. Check **Elastic** [http://localhost:9200/](http://localhost:9200/) with un _elastic_ and password _changeme_ renders:
   ```json
   {
    "name" : "elasticsearch",
    "cluster_name" : "docker-cluster",
    "cluster_uuid" : "KCWFYj4qRPGe5ZBgA6dlTg",
    "version" : {
    "number" : "9.4.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "c402c2b36d90eae29c0182f86bd9050fd0b746cc",
    "build_date" : "2026-05-25T22:10:36.017759931Z",
    "build_snapshot" : false,
    "lucene_version" : "10.4.0",
    "minimum_wire_compatibility_version" : "8.19.0",
    "minimum_index_compatibility_version" : "8.0.0"
    },
    "tagline" : "You Know, for Search"
   }
   ```
6. Check **Kibana** [http://localhost:5601/](http://localhost:5601/) again with un _elastic_ and password _changeme_
   after logging in we come to a home page: