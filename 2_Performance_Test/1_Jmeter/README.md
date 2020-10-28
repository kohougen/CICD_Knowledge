# Jmeter
Apache JMeter application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance.
* [Home Site](https://jmeter.apache.org/index.html)
* [Download](https://jmeter.apache.org/download_jmeter.cgi)
* [Jmeter Functions](https://jmeter.apache.org/usermanual/functions.html)
* [Jmeter command-line options](https://jmeter.apache.org/usermanual/get-started.html#options)

## How To Use [link](https://qiita.com/atsu_kg/items/1ff4ff13b8f30c3114b1)
1. Create Test Plan (File > New)
1. Create Test Cases
   * Create Thread Group (Right click TestPlan > Add > Treads(Users) > Thread Group)
   * Create HTTP Request (Right click Thread Group > Add > Sampler > HTTP Request)
1. Config Element
   * Create a HTTP Header Manager (Right click Thread Group > Add > Config Element > HTTP Header Manager)
   * Create a Authorization Manager (Right click Thread Group > Add > Config Element > HTTP Authorization Manager)
1. Create Test Result Report
   * Tree Report (Right click Thread Group > Add > Listener > View Results Tree)
   * Table Report (Right click Thread Group > Add > Listener > View Results Table)
   * Aggregate Report (Right click Thread Group > Add > Listener > Aggregate Report)
1. Run Test

## Sample Performance Test(test login api with AWS API Gateway)
1. Launch Up Jmeter With GUI Mode
   * No Proxy: Double Click bin\jmeter.bat To
   * With Proxy: Run The Following Command
      * -H: Proxy server
      * -P: Proxy server port
      * -u: username for proxy server
      * -a: password for proxy server
      ```shell
      .\bin\jmeter -H host -P port -u username -a password
      ```
1. Follow The Steps In 'How To Use' To Create A Test Plan And A Test Case
1. Create A User Parameters And Set The Following Information
Name | Value
--------------- | -------------------------------------------------------------------------------
split_user_info | ${__split(${__StringFromFile(E:\\tool\\jmeter\\testPlan\\userList.txt)}, USER)}
username        | ${USER_1}
password        | ${USER_2}
   * ${__StringFromFile(filePath)}: Get String List From File
   * ${__split(stringToSplit, VAR): Split The `stringToSplit` Set The Result To `VAR`, You Can Use `VAR_1` to get the first subString, use `VAR_2` to get the second one.

![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/Pictures/User_Parameters.PNG)

1. Create Test User List File And Add Some Records 
![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/Pictures/userList.PNG)

1. Set The Following Information In HTTP Request
   * Protocol: https
   * Sever Name or IP: API Gateway's invoke URL
   * PortNumber: 443
   * HTTP Request: POST (according to the test api)
   * Path: test api's path
   * Content Encoding: UTF-8
   * Request Body Data: login information(${username} and ${password} are variables which defined in 'User Parameters')

![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/Pictures/HTTP_Request.PNG)

1. Follow The Steps In 'How To Use' To Create Test Result Report
1. Set Thread Properties In Thread Group To Confirm If The Test Case Works Well
   * Number of Threads(users): Number of users to simulate
   * Ramp-up period(seconds): How long JMeter should take to get all the threads started
   * Loop Count: Number of times to perform the test case
     * "infinite" can be selected causing the test to run until manually stopped or end of the thread lifetime is reached

![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/Pictures/ThreadGroup.PNG)

1. Run The Test Plan In GUI Mode To Confirm If Everything Is OK(Right click Thread Group > Start)
1. Confirm Test Result(Request Head/Body And Response Head/Body)

![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/Pictures/Test_Result.PNG)

1. Add More Test Data And Update Thread Properties For The Real Performance Test(Set A Big Number)
1. Save Test Plan(File > Save TestPlan as)
1. Run The Performance Test In Command Mode
   * No Proxy: Run The Following Command
      * -n: run JMeter in nongui mode
      * -t: the jmeter test(.jmx) file to run
      * -l: the file to log samples to
      * -j: jmeter run log file
      ```shell
      bin\jmeter -n -t path_of_testplan_file\xxx.jmx -l path_of_testplan_log\ -j path_of_jmeter_log\jmeter.log
      ```
   * With Proxy: Run The Following Command
      ```shell
      bin\jmeter -n -t path_of_testplan_file\xxx.jmx -l path_of_testplan_log\ -j path_of_jmeter_log\jmeter.log -H host -P port -u username -a password
      ```
1. Confirm Test Log
   * Testplan Log
   ```log
   timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
   1603856175019,2337,HTTP リクエスト,200,OK,loginテスト 1-1,text,true,,2138,341,2,2,https://xxx.execute-api.ap-northeast-1.amazonaws.com/dev/api/auth/login,2333,0,30
   1603856176438,1064,HTTP リクエスト,200,OK,loginテスト 1-2,text,true,,2023,341,1,1,https://xxx.execute-api.ap-northeast-1.amazonaws.com/dev/api/auth/login,1064,0,5
   1603856177943,801,HTTP リクエスト,500,Internal Server Error,loginテスト 1-3,text,false,,755,341,1,1,https://xxx.execute-api.ap-northeast-1.amazonaws.com/dev/api/auth/login,801,0,9
   ```

   * JMeter Log
   ```log
   2020-10-28 12:36:14,629 INFO o.a.j.JMeter: Creating summariser <summary>
   2020-10-28 12:36:14,636 INFO o.a.j.e.StandardJMeterEngine: Running the test!
   2020-10-28 12:36:14,636 INFO o.a.j.s.SampleEvent: List of sample_variables: []
   2020-10-28 12:36:14,636 INFO o.a.j.s.SampleEvent: List of sample_variables: []
   2020-10-28 12:36:14,641 INFO o.a.j.e.u.CompoundVariable: Note: Function class names must contain the string: '.functions.'
   2020-10-28 12:36:14,641 INFO o.a.j.e.u.CompoundVariable: Note: Function class names must not contain the string: '.gui.'
   2020-10-28 12:36:14,892 INFO o.a.j.f.StringFromFile: setParameters(E:\\tool\\jmeter\\testPlan\\userList.txt)
   2020-10-28 12:36:14,907 INFO o.a.j.JMeter: Running test (1603856174907)
   2020-10-28 12:36:14,932 INFO o.a.j.e.StandardJMeterEngine: Starting ThreadGroup: 1 : loginテスト
   2020-10-28 12:36:14,932 INFO o.a.j.e.StandardJMeterEngine: Starting 3 threads for group loginテスト.
   2020-10-28 12:36:14,932 INFO o.a.j.e.StandardJMeterEngine: Thread will continue on error
   2020-10-28 12:36:14,932 INFO o.a.j.t.ThreadGroup: Starting thread group... number=1 threads=3 ramp-up=3 delayedStart=true
   2020-10-28 12:36:14,933 INFO o.a.j.t.ThreadGroup: Started thread group number 1
   2020-10-28 12:36:14,933 INFO o.a.j.e.StandardJMeterEngine: All thread groups have been started
   2020-10-28 12:36:14,939 INFO o.a.j.t.JMeterThread: Thread started: loginテスト 1-1
   2020-10-28 12:36:14,941 INFO o.a.j.f.StringFromFile: loginテスト 1-1 opening file E:\tool\jmeter\testPlan\userList.txt
   2020-10-28 12:36:14,956 INFO o.a.j.p.h.s.HTTPHCAbstractImpl: Local host = C010362914
   2020-10-28 12:36:14,961 INFO o.a.j.p.h.s.HTTPHC4Impl: HTTP request retry count = 0
   2020-10-28 12:36:14,963 INFO o.a.j.s.SampleResult: Note: Sample TimeStamps are START times
   2020-10-28 12:36:14,963 INFO o.a.j.s.SampleResult: sampleresult.default.encoding is set to ISO-8859-1
   2020-10-28 12:36:14,963 INFO o.a.j.s.SampleResult: sampleresult.useNanoTime=true
   2020-10-28 12:36:14,963 INFO o.a.j.s.SampleResult: sampleresult.nanoThreadSleep=5000
   2020-10-28 12:36:15,075 INFO o.a.j.p.h.s.h.LazyLayeredConnectionSocketFactory: Setting up HTTPS TrustAll Socket Factory
   2020-10-28 12:36:15,081 INFO o.a.j.u.JsseSSLManager: Using default SSL protocol: TLS
   2020-10-28 12:36:15,081 INFO o.a.j.u.JsseSSLManager: SSL session context: per-thread
   2020-10-28 12:36:15,722 INFO o.a.j.u.SSLManager: JmeterKeyStore Location:  type JKS
   2020-10-28 12:36:15,723 INFO o.a.j.u.SSLManager: KeyStore created OK
   2020-10-28 12:36:15,723 WARN o.a.j.u.SSLManager: Keystore file not found, loading empty keystore
   2020-10-28 12:36:16,437 INFO o.a.j.t.JMeterThread: Thread started: loginテスト 1-2
   2020-10-28 12:36:17,358 INFO o.a.j.t.JMeterThread: Thread is done: loginテスト 1-1
   2020-10-28 12:36:17,358 INFO o.a.j.t.JMeterThread: Thread finished: loginテスト 1-1
   2020-10-28 12:36:17,502 INFO o.a.j.t.JMeterThread: Thread is done: loginテスト 1-2
   2020-10-28 12:36:17,502 INFO o.a.j.t.JMeterThread: Thread finished: loginテスト 1-2
   2020-10-28 12:36:17,940 INFO o.a.j.t.JMeterThread: Thread started: loginテスト 1-3
   2020-10-28 12:36:18,746 INFO o.a.j.t.JMeterThread: Thread is done: loginテスト 1-3
   2020-10-28 12:36:18,746 INFO o.a.j.t.JMeterThread: Thread finished: loginテスト 1-3
   2020-10-28 12:36:18,748 INFO o.a.j.e.StandardJMeterEngine: Notifying test listeners of end of test
   2020-10-28 12:36:18,754 INFO o.a.j.r.Summariser: summary =      3 in 00:00:04 =    0.8/s Avg:  1400 Min:   801 Max:  2337 Err:     1 (33.33%)
   2020-10-28 12:36:18,758 INFO o.a.j.f.StringFromFile: StandardJMeterEngine closing file E:\tool\jmeter\testPlan\userList.txt
   ```