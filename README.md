# Prometheus-query-results-as-CSV
We can query Prometheus data via API. for an example to query data for metric named CPU, you can use following API

http://prom_server:9090/api/v1/query?query=cpu

or if you need data for past 1 hour then add filters like [1h] or [1m] etc.

http://prom_server:9090/api/v1/query?query=cpu[1h]

sample output

{"status":"success","data":{"resultType":"vector","result":[{"metric":{"__name__":"collectd_cpu","cpu":"0","instance":"overcloud-cephstorage-0.localdomain","job":"collectd","service":"idle"},"value":[1528895820.304,"2033227691"]},

Now this is very tedious job if we have 100's of metrics and if need to go over each metric names and query them individually and export to a file .So I used a python script based on Robust Perception blog on query result as CSV.

and modified the script to query all metric names and then query individual metrics with this list of metric names and save to a file. Now, this can be run as a cron job configured to run hourly. The python script will get last 1 hours of data and put it in an archive file.
