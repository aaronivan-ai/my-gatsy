## 關於Apache Airflow

### 歸屬於「Workflow engine」

* 主要是data management層次的workflow
  * Data engineering領域工具箱之一
* 用pipeline或graph的角度來組合task
  * Conductor等都是類似的做法
* 非BPMN表示法

### Open source workflow engines[https://github.com/meirwah/awesome-workflow-engines]

### 功能

* 支援DAG流程
  * 不支援有循環的流程 (Not support cyclic graph)
* 由於是直接寫Python程式，只要Python有支援，都能實作出對應的功能
  * 內建許多operator，如bash, db operator
* 支援排程，backfill
* 支援Task retry
* 支援多樣Task的串接
  * Branching
  * Conditional task
  * 動態建立多個task，做到類似平簽
  * Trigger rule (從upstream task的狀態，決定downstream task是否能執行)
* 提供Sensor機制，透過接收event, action來決定下一步
  * Airflow中的術語是poking(也就是用polling的方式)，來檢查sensor的條件是否成立
  * 可用來實作類似Human task
* TriggerDagRunOperator可做到呼叫subflow的效果
* 提供REST, CLI，啟動workflow
* 支援與多樣的外部系統溝通
  * 如Apache Spark，多種public cloud provider
* 內建Obervability
* 提供失敗的告警機制，支援定義SLA
* Scalable
  * 多個task scheduler, task executor
  * 使用DB lock機制
* Security capability built-in
* Kubernetes ready
* Cloud solution ready

### 挑戰

* 複雜度考量
  * 多種元件要架設：webserver, scheduler, database和DAG要怎麼管理
* 這是個需要有穩定，值得信任的infra的框架
  * Apache airflow裡的metastore，需要用資料庫，目前支援的有MySQL, PostgreSQL，但這在gg的K8S中很不穩
* Apache airflow適合做各種整合流程的workflow，針對有許多Human task的workflow是否適用，需要再驗證
