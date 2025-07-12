# Analisi ARP/DHCP

Questa cartella contiene le query Splunk e le relative visualizzazioni per l'analisi dei protocolli ARP e DHCP

---

## Query 1: Analisi delle Richieste ARP con Destinazione MAC Null


```spl
index=botsv3 sourcetype=stream:arp arp_dest_mac="00:00:00:00:00:00"
| eval pair = src_ip . "->" . dest_ip
| stats count by pair
| sort – count
```
![Descrizione dell'immagine](img/analisi_richieste_destinazione_MAC_nullo.png)

---

## Query 2: Distribuzione del Traffico ARP per Tipo di Operazione

```spl
index=botsv3 sourcetype=stream:arp 
| stats count by opcode 
| sort – count
```
![Descrizione dell'immagine](img/traffico_arp_per_operazione.png)

---

## Query 3: Top Host per Traffico ARP Generato


```spl
index=botsv3 sourcetype=stream:arp 
| stats count by src_ip 
| sort - count 
| head 35

```
![Descrizione dell'immagine](img/top_host_traffico_arp.png)

---

## Query 4: Distribuzione dei Messaggi DHCP per Tipo di Operazione

```spl 
index=botsv3 sourcetype=stream:dhcp 
| stats count by opcode 
| sort – count
```
![Descrizione dell'immagine](img/distribuzione_messaggi_dhcp.png)

---

## Query 5: Configurazione dei Server DHCP

```spl 
index=botsv3 sourcetype=stream:dhcp
| stats avg(ip_lease_time) as avg_lease_time, values(domain_name{}) as domains, values(dns_server{}) as dns_servers by dest_ip
| sort - avg_lease_time

```
![Descrizione dell'immagine](img/configurazione_serve_dhcp.png)

---
## Query 6: Assegnazione degli Indirizzi IP tramite DHCP

```spl 
index=botsv3 sourcetype=stream:dhcp 
| stats count by yiaddr, chaddr
| sort – count

```
![Descrizione dell'immagine](img/assegnazione_ip_tramite_dhcp.png)

---













