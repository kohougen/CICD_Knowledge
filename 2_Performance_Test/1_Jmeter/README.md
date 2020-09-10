# Jmeter
Apache JMeter application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance.
* [Home Site](https://jmeter.apache.org/index.html)
* [Download](https://jmeter.apache.org/download_jmeter.cgi)

## How To Use [link](https://qiita.com/atsu_kg/items/1ff4ff13b8f30c3114b1)
1. Create Test Plan (File > New)
1. Create Thread Group (Right click TestPlan > Add > Treads(Users) > Thread Group)
1. Create Test Cases
   * Create HTTP Request (Right click Thread Group > Add > Sampler > HTTP Request)
1. Config Element
   * Create a HTTP Header Manager (Right click Thread Group > Add > Config Element > HTTP Header Manager)
   * Create a Authorization Manager (Right click Thread Group > Add > Config Element > HTTP Authorization Manager)
1. Create Test Result Report
   * Tree Report (Right click Thread Group > Add > Listener > View Results Tree)
   * Table Report (Right click Thread Group > Add > Listener > View Results Table)
   * Aggregate Report (Right click Thread Group > Add > Listener > Aggregate Report)