# Analisi Protocollo IP

Questa sezione contiene le query Splunk utilizzate per analizzare il traffico IP nel dataset BOTSv3, con le relative visualizzazioni.

---

## Query 1: Volume traffico per protocollo

```spl
index=botsv3 sourcetype=stream:ip
| stats sum(bytes) as total_bytes by protocol
| where total_bytes > 5
```
!(img/volume_traffico_per_protocollo.png)  
