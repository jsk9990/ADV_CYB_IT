# Analisi ARP/DHCP

Questa cartella contiene le query Splunk e le relative visualizzazioni per l'analisi dei protocolli ARP e DHCP, come descritto nella sezione 3.2 della relazione.

---

## Query 1: Analisi delle Richieste ARP con Destinazione MAC Null


```spl
index=botsv3 sourcetype=stream:arp arp_dest_mac="00:00:00:00:00:00"
| eval pair = src_ip . "->" . dest_ip
| stats count by pair
| sort – count

