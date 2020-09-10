# Jmeter
Apache JMeter application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance.
* [Home Site](https://jmeter.apache.org/index.html)
* [Download](https://jmeter.apache.org/download_jmeter.cgi)

## How To Use [link](https://qiita.com/atsu_kg/items/1ff4ff13b8f30c3114b1)
1. Create a test plan (File > New)
1. Create a thread group (Right click TestPlan > Add > Treads(Users) > ThreadGroup)
1. Create Test Cases
   1. Create HTTP Request (Right click ThreadGroup > Add > Sampler > HTTP Request)
1. Config Element
   1. Create a HTTP Header Manager (Right click ThreadGroup > Add > Config Element > HTTP Header Manager)
   1. Create a Authorization Manager (Right click ThreadGroup > Add > Config Element > HTTP Authorization Manager)
1. Create Test Result Report
   1. Tree Report (Right click ThreadGroup > Add > Listener > View Results Tree)
   1. Table Report (Right click ThreadGroup > Add > Listener > View Results Table)
   1. Aggregate Report (Right click ThreadGroup > Add > Listener > Aggregate Report)