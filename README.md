# metrix

Metrics collector written in golang

## Requirements

You need to have go 1.1 and some build tools installed. This can be done in ubuntu like this (make sure `universe` is enabled):
	
	apt-get install -y bzr git-core build-essential
	cd /opt
	curl -OL https://go.googlecode.com/files/go1.1.1.linux-amd64.tar.gz
	tar xvfz go1.1.1.linux-amd64.tar.gz
	export GOROOT=/opt/go
	export GOPATH=/go

## Installation
    
Building of the binary needs to only be done once. You can just copy it to any linux system and run it without any extra dependencies.

    git clone git@github.com:dynport/metrix.git /tmp/metrix
    cd /tmp/metrix
    make install_dependencies
    make
    make install    


## Examples

    # Post load and memory metrics to opentsdb
    metrix --memory --loadavg --opentsdb=<opentsdbhost>:<opentsdbport>

    # Post memory and loadavg metrix to opentsdb (every 60s), log output to syslog
    # 
    # /etc/cron.d/metrix
    * * * * * root /usr/local/bin/metrix --memory --loadavg --opentsdb=<opentsdbhost>:<opentsdbport> 2>&1 | logger -t metrix

## Help

    USAGE: metrix
      --help           	Print this usage page                                               
      --keys           	Only list all known keys                                            
      --opentsdb       	Report metrics to OpenTSDB host.                                    
                        EXAMPLE: opentsdb.host:4242                                         

      --graphite       	Report metrics to Graphite host.                                    
                        EXAMPLE: graphite.host:2003                                         

      --hostname       	Hostname to be used for tagging. If blank the local hostname is used
      --net            	Collect network metrics                                             
      --df             	Collect disk free space metrics                                     
      --disk           	Collect disk usage metrics                                          
      --cpu            	Collect cpu metrics                                                 
      --processes      	Collect metrics for processes                                       
      --loadavg        	Collect loadvg metrics                                              
      --memory         	Collect memory metrics                                              
      --nginx          	Collect nginx metrics                                               
                        DEFAULT: http://127.0.0.1:8080                                      

      --redis          	Collect redis metrics                                               
                        DEFAULT: 127.0.0.1:6379                                             

      --elasticsearch  	Collect ElasticSearch metrics                                       
                        DEFAULT: http://127.0.0.1:9200/_status                              

      --riak           	Collect riak metrics                                                
                        DEFAULT: http://127.0.0.1:8098/stats                                

      --pgbouncer      	Collect pgbouncer metrics                                           
                        DEFAULT: 127.0.0.1:6432                                             

      --postgres       	Collect postgres metrics.                                           
                        EXAMPLE: psql://user:pwd@host/db                                    
