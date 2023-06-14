Docker siege
---
Docker image containing [siege](https://github.com/JoeDog/siege), an open source regression test
and benchmark utility to perform stress tests.

## How use it
Build the docker image
```
docker build -t siege:latest .
```

Go inside the docker container (an Ubuntu one) mounting the directory files into the home
```
docker run --rm -it -v ${PWD}/files:/home siege:latest bash
```
Run siege, i.e.
```
siege -b -c 100 -i -r once -v -f stagingUrls.csv --no-parser --no-follow
```
This example command takes as input a csv files containing a list of urls and perform 100 concurrent calls to the urls.
The output provides those metricsa
```
root@dfe7b9a9735e:/home# siege -b -c 100 -i -r once -v -f stagingUrls.csv --no-parser --no-follow
New configuration template added to /root/.siege
Run siege -C to view the current settings in that file
^C
{       "transactions":                          156,
        "availability":                        99.36,
        "elapsed_time":                        15.83,
        "data_transferred":                     1.72,
        "response_time":                        7.08,
        "transaction_rate":                     9.85,
        "throughput":                           0.11,
        "concurrency":                         69.74,
        "successful_transactions":               153,
        "failed_transactions":                     1,
        "longest_transaction":                 15.26,
        "shortest_transaction":                 0.52
}

```