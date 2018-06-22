# anyuzhangpuzzle_2018


## Table of Contents
1. [Implementation details](README.md#implementation-details)
2. [Test 1](README.md#test-1)
3. [My tests](README.md#my-tests)
4. [Optimization of sessionization.py ](README.md#Optimization-of-sessionization.py )

## Implementation details

The algorithm in sessionization.py uses two dictionaries iplib and timelib. The iplib stores ip of unexpired session as key and [first request time, most recent request time, num of requests] as value.  The timelib is an OrderedDict and stores timestamp as key and all ips that have a most recent request at that timestamp as value.   Due to the chronical order of log.csv, all keys in timelib are inserted chronically.  Maintaining this order will boost the process of deleting timed-out sessions compared with normal dictionary structure.  As inactivity period time rises, the performance gap between my origianl version of sessionization.py and optimized version of sessionization.py will increase.

## Test 1
Pass test_1  

The result generated by my sessionization.py is exactly same as the file saved in the test output.
In the processing of generating sessionization.txt, I found the datasets from website varies in the format of time. 
The test_1 provide us time format as 2017-06-30 ,but onine log.csv 's time format is 12/31/03.  

## My tests

### Log.csv

From the website SEC weblogs I can access to a lot of datasets, I picked sample datasets at one day from 2003 to 2017. The datasets varied a lot from 106kB to 2.78GB, which is beneficial to checking the performance of my sessionization.py on small and large datasets. But the git hub only allow me upload files smaller than 25 MB. So what you can access in tests folder are just small datasets.

### inactivity_period.txt

From the details of challange I know the duration is a important value to check if an IP is in a session of a single web page document request. The value will range from 1 to 86,400 (i.e., one second to 24 hours). In the given test example, the duration time is 2 seconds. By increasing the duration time : 2 seconds , 3seconds and 100 seconds, the computing time of output file increased also. 
By setting the period of inactivity to 5 seconds, with same log.csv in the test_1, the output is changed as following:

    101.81.133.jja,2017-06-30 00:00:00,2017-06-30 00:00:00,1,1
    107.23.85.jfd,2017-06-30 00:00:00,2017-06-30 00:00:03,4,4
    108.91.91.hbc,2017-06-30 00:00:01,2017-06-30 00:00:04,4,2
    106.120.173.jie,2017-06-30 00:00:02,2017-06-30 00:00:02,1,1
    107.178.195.aag,2017-06-30 00:00:02,2017-06-30 00:00:04,3,2
    
As I changed the period of inactivity time to 5 seconds, two sessions of 108.91.91.hbc combined to one session. 

## Optimization of sessionization.py 

With a large dataset in 2017, which size is 2.78GB, the computating time is as long as more than 20 mins in the first version of my sessionization.py. It is too long to be a applicable program. So I made changes in the data structure of inputs. Then as following example, the computational time can be half of original version.



    For checking the performence of optimized sessionization method, I used the 455.9MB dataset in 06/29/2011 with 100s duration time. 
    original                          optimized 
    real	6m3.742s                  real	3m17.475s
    user	6m0.968s                  real	3m17.475s
    sys	0m1.282s                  sys	0m1.084s



