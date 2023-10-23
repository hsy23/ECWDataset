# Edge Cloud servers Workload Dataset（ECWDataset）
In this Github repo, we provide several datasets could be used for the dynamic sequence time-series problem. All datasets have been preprocessed and they were stored as .npy files. The dataset ranges from 2022/08 to 2022/10. 

**Data background:** The ECW is a real-world dataset utilized in our study [One for All: Unified Workload Prediction for Dynamic Multi-tenant Edge Cloud Platforms](https://github.com/hsy23/KDD23_DynEformer). The whole dataset encompasses diverse load logs (e.g., **bandwidth for ECW**, CPU, storage) and abundant cross-domain static data from a leading edge cloud service company that provides mature idle computing resource integration and edge cloud resource provisioning.

*Dataset list* (updating)

- [x] **ECW-08**: A matrix shaped as **797 $ \times $ 720 $\times$ 16** represents the upload bandwidth workload variation of 797 edge servers over 720 hours (24\*30) in 2022/08. 16 is the feature dimension of the data, containing 4-dimensional dynamic features and 12-dimensional static content features from the cross domain. 

- [x] **ECW-09**: A matrix shaped as **1022 $\times$ 720 $\times$ 16** represents the upload bandwidth workload variation of 1022 edge servers over 720 hours (24\*30) in 2022/09.

- [ ] ECW-min: Workload logs with a granularity of every 5 minutes of upload bandwidth, allows for finer granularity load changes compared to ECW.

The following dataset is recommended for testing.

- [ ] **ECW-App-Switch-sample**: The workload series where application switching occurred during 2022/08/25-2022/08/30. The exact time of application switches can be easily detected by plotting the curve, as it is accompanied by a sudden change in the load change pattern. *If you wish to test the model's capability to handle abrupt changes in time-series patterns (extreme concept-drift), use this dataset.*

- [ ] **ECW-New-App**: The workload series of the applications that never appeared in ECW-08. If you wish to test the model's generalizability when faced with unknown time-series patterns, use this dataset.

- [ ] **ECW-New-Infras**.: The workload series running on infrastructure that has never been present in the ECW.

If you use this dataset please cite the work DynEformer @ KDD2023 [\[paper\]](https://arxiv.org/abs/2306.01507), [\[code\]](https://github.com/hsy23/KDD23_DynEformer) (The Bibtex version is comming soon):

> Shaoyuan Huang, Zheng Wang, Heng Zhang, Xiaofei Wang, Cheng Zhang, and Wenyu Wang. 2023. One for All: Unified Workload Prediction for Dynamic Multi-tenant Edge Cloud Platforms. In Proceedings of the 29th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD ’23), August 6–10, 2023, Long Beach, CA, USA. ACM, New York, NY, USA, 10 pages. https://doi.org/10.1145/3580305.3599453

## Why Cross-domain Static Content is involved in ECW?
The cross-domain data points, which encompass 12 dimensions of static server hardware attributes, including maximum bandwidth, number of CPUs, location, and other infrastructure characteristics. This data is collected when edge servers join the Multi-tenant Edge Cloud Platforms(MT-ECP) or during subsequent updates. Incorporating cross-domain data is aimed to further enhance model's robustness, as noted in previous research (Lim et al. [a]). Specifically, for workload prediction in MT-ECP, server features such as hardware attributes and geographical location significantly influence workload variations.

[a] Bryan Lim, et al. "Temporal Fusion Transformers for interpretable multi-horizon time series forecasting". International Journal of Forecasting, 2021

## ECW and its derivative data:
ECW, ECW-App-Switch, ECW-New-App, ECW-New-Infras cover all three types of behavior of dynamic MT-ECP, as shown in the following figure, all datasets are shaped as **N(edge server num)\*T(series len, hourly granularity)\*F(num of feature dimensions, all 16)**. 


<div align="center">
  <img src="https://github.com/hsy23/ECWDataset/assets/45703329/c08fb4d2-42da-4dc5-969d-266c99d69cc1">
  <p>Figure 1.Workloads under dynamic MT-ECP behaviors.</p>
</div>

Specifically, each edge server's workload incorporates daily short-term perodical patterns and weekly long-term perodical patterns (where future load on the same calendar day of the upcoming week resembles that of the current day's load), in addition to certain trend patterns and irregular fluctuations. Due to the heterogeneity in server attributes and application patterns, these patterns vary across different load series. Compared to existing time-series prediction datasets (such as [ETT](https://github.com/zhouhaoyi/ETDataset) and [Azure](https://github.com/Azure/AzurePublicDataset/)), ECW exhibits more complex patterns and higher-frequency dynamics (application switch disruptions and new entities), significantly elevating the generalization requirements for models.

We use the .npy file format to save the data, an edge server workload demo of the ECW data is illustrated in Figure 2. The first line (16 columns) is the horizontal header and includes "bw_upload", "hour", "day", "week", 'province', 'bandwidth_type', 'nat_type', 'isp', 'billing_rule', 'upbandwidth', 'upbandwidth_base', 'cpu_num', 'memory_size', 'disk_size', 'test_sat', and 'loss_sat'. The detailed meaning of each column name is shown in the Table 1.

<div align="center">
  <img src="https://github.com/hsy23/ECWDataset/assets/45703329/5b7189dd-71f0-4097-b945-bdbf51ef43aa">
  <p>Figure 2. Edge server workload demo.</p>
</div>

| Field | bw_upload | hour | day | week | province | bandwidth_type | nat_type | isp | billing_rule | upbandwidth | upbandwidth_base | cpu_num | memory_size | disk_size | test_sat | loss_sat |
| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----:| :----: | :----: | :----: | :----: | :----:| :----: | :----: |
| Description | upload bandwidth workload (target) | record time (dynamic features) | <- | <- | edge server location | quality assessment of the network | nat type | isp | types of billing | total server bandwidth | available server bandwidth | cpu_num | memory_size | disk_size | network pressure test quality | packet loss quality |



<p align="center"><b>Table 1.</b> Description for each columm.</p>

