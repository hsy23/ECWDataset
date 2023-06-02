# Edge Cloud servers Workload Dataset（ECWDataset）
In this Github repo, we provide several datasets could be used for the dynamic sequence time-series problem. All datasets have been preprocessed and they were stored as .csv files. The dataset ranges from 2022/08 to 2022/10. 

**Data background:** The ECW is a real-world dataset utilized in our study [One for All: Unified Workload Prediction for Dynamic Multi-tenant Edge Cloud Platforms](https://github.com/hsy23/KDD23_DynEformer). The whole dataset encompasses diverse load logs (e.g., **bandwidth for ECW**, CPU, storage) and abundant cross-domain static data (For example, the hardware properties and geographical location of servers) from a leading edge cloud service company that provides mature idle computing resource integration and edge cloud resource provisioning. The company integrates 100+ different resource providers (totaling 5000+ servers distributed nation-wise) and serves 40+ typical content providers by deploying 60,000+ application instances to cater to 70+ million users.

*Dataset list* (updating)

- [x] ECW-08: A matrix shaped as **797 $\times$ 720 $\times$ 16** represents the upload bandwidth workload variation of 797 edge servers over 720 hours (24\*30) in 2022/08. 16 is the feature dimension of the data, containing 4-dimensional dynamic features and 12-dimensional static content features from the cross domain. 

- [x] ECW-09: A matrix shaped as **1022 $\times$ 720 $\times$ 16** represents the upload bandwidth workload variation of 1022 edge servers over 720 hours (24\*30) in 2022/09.

<div align="center">
  <img src="https://github.com/hsy23/ECWDataset/assets/45703329/5b7189dd-71f0-4097-b945-bdbf51ef43aa">
  <p>Figure 2.The process of building the global pool.</p>
</div>
