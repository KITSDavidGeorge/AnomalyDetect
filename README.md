# AnomalyDetect
The current version of `AnomalyDetect` detects anomalous heart rate from smartwatch data. `AnomalyDetect` can be used with either RHR (Resting Heart Rate) or HROS (Heart Rate Over Steps) as an input. This method can be applied to any smartwatch data like FitBit, Apple, Garmin and Empatica.


#### Install required packages

```
pip install -r requirements.txt
```


## Offline Models 

Offline models use all the data to find anomalies.

#### RHR-AD (Resting Heart Rate) Offline Anomaly Detector

Full command 
```
python rhrad_offline.py \
       --heart_rate hr.csv \
       --steps steps.csv \
       --myphd_id id_offline \
       --figure id_offine.pdf \
       --anomalies id_offline_anomalies.csv \
       --symptom_date 2020-01-30 \
       --diagnosis_date 2020-01-31 \
       --outliers_fraction 0.1 \
       --random_seed 10 
 ```
 

#### HROS-AD (Heart Rate Over Steps) Offline Anomaly Detector

Full command 
```
python hrosad_offline.py \
       --heart_rate hr.csv \
       --steps steps.csv \
       --myphd_id id_offline \
       --figure id_offine.pdf \
       --anomalies id_offline_anomalies.csv \
       --symptom_date 2020-01-30 \
       --diagnosis_date 2020-01-31 \
       --outliers_fraction 0.1 \
       --random_seed 10 
 ```
 
 

## Online Model

Online model uses RHR data and splits it into training data by taking the first 744 hours as a baseline (1 month) and testing data by taking the next 1 hour data, and uses a sliding window of length 1 hour to find anomalies in the test data. If the anomalies occur frequently with in 12 hours, it will automatically create warning (yellow) and serious (red) alerts at every 6 A.M and 6 P.M.

Full command
```
python rhrad_online_alerts.py --heart_rate pbb_fitbit_oldProtocol_hr.csv \
       --steps pbb_fitbit_oldProtocol_steps.csv \
       --myphd_id pbb_RHR_online \
       --figure1 pbb_RHR_online_anomalies.pdf \
       --anomalies pbb_RHR_online_anomalies.csv \
       --symptom_date 2020-01-10 --diagnosis_date 2020-01-11 \
       --outliers_fraction 0.1 \
       --random_seed 10  \
       --baseline_window 744 --sliding_window 1 
       --alerts pbb_RHR_online_alerts.csv \
       --figure2 pbb_RHR_online_alerts.pdf
```
