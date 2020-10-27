# Jmeter
Apache JMeter application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance.
* [Home Site](https://jmeter.apache.org/index.html)
* [Download](https://jmeter.apache.org/download_jmeter.cgi)

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

## Sample Performance Test(test login api with userList file)
1. Double Click bin\jmeter.bat To Launch Up Jmeter With GUI Mode
1. Follow The Steps In 'How To Use' To Create A Test Plan And A Test Case
![alt text](https://github.com/kohougen/CICD_Knowledge/blob/master/2_Performance_Test/1_Jmeter/HTTP_Request.png)

