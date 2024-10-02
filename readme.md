# Overall Information

`DDCSTrain+.txt` and `DDCSTest+.txt` are copies of original files in NSL-KDD dataset.

`NSLKDD_mrtipk.ipynb` is mrtipk solution without changes. It fails in KNN algorithm.


`ibm_watson_deployed.ipynb` is the effort to hit the endpoint to solution from IBM Auto AI on the original modified NSL-KDD ( I think it was the data with attack_state as target (normal 0 else 1) no normalization and no  one hot encoding)

#  Adding graph features:

## 1.Generate Graph based IP addresses
### generate_ips.ipynb
### generate_ips_privacy.ipynb

output(s):
* generated_ips.csv
* generated_ips_privacy.csv
* community_graph.html
* community_graph_privacy.html

## 2.Add IP addresses as features to the NSL-KDD
### enrich_NSLKDD_with_IPs.ipynb 

inputs:

* KDDTrain+.txt (NSL-KDD dataset)
* KDDTest+.txt (NSL-KDD dataset)
* features.txt (NSL-KDD dataset)
* generated_ips.csv (previously generated - deprecated)
* * generated_ips_privacy.csv (previously generated)

outputs:
* csv files for Train and Test data. `train_ip_config_A.csv` and `test_ip_config_A.csv`
* ip_src and ip_dest are added into NSL-KDD dataset.
config_A stands for a version of configuration on how IP addresses are generated.

## 3. Show relations between IP addresses 
`generated_ips_visualize.ipynb` visualizes relations between ip_src and ip_desc 

## 4.Run e2e 
`NSLKDD_IP.ipynb` is a modified version of `NSLKDD_mrtipk.ipynb`. Changes are made just to handle `ip_src` and `ip_dest` columns.
`NSLKDD_IP.ipynb` shows that IP addresses are not selected as the first 50 features by themselves.
For that reason ML training is not executed.



### 5. Extract centralities of a DiGraph with ip_src and ip_dest
`generated_ips_mining.ipynb` calculates centralities (, and communities) for each IP and appends mining results to test and train data.

outputs:
* train_data_ip_config_A_centralities.csv
* test_data_ip_config_A_centralities.csv

## 6.Re-run e2e with the centrality data

NSL_KDD_IP_centrality.ipynb