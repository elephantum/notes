# Что жрет бабло 2025-03
[Billing](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;projects=holybricks?project=holybricks)
* Cloud Storage: $4.3K
	* кронджобы гоняют трафик (картинки)
		* Data transfer GCP Multi-region: $2.33K
		* Multi-Region Standard Class A Operations: $709
		* Multi-Region Standard Class B Operations $109
	- раздача статики
		* Download worldwide: $745
		* Download APAC $79
		* Download Australia $22
	* хранение
		* Standard Storage US Multi-region: $336
	* [Billing - Cloud Storage](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;grouping=GROUP_BY_SKU;projects=holybricks;products=services%2F95FF-2EF5-5EA1?project=holybricks)
* Compute Engine: $2.9K
	* Кластер
		* E2 Instance Core running in Americas $1K
		* E2 Instance Ram running in Americas $565
		* Network Inter Zone Data Transfer Out $137
		* Balanced PD Capacity $101
		* Network Internet Data Transfer Out from Americas to EMEA $93
		* Network Internet Data Transfer Out from Americas to Americas $76
		* Regional Storage PD Capacity $64
	* inference
		* Nvidia Tesla T4 GPU running in Americas $521
		* N1 Predefined Instance Core running in Americas $94
	* [Billing - Compute Engine](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;grouping=GROUP_BY_SKU;projects=holybricks;products=services%2F6F81-5844-456A?project=holybricks)
* Cloud SQL: $1.9K
	* Cloud SQL for PostgreSQL: Zonal - vCPU in Americas $521
	* Cloud SQL for PostgreSQL: Zonal - Standard storage in Americas $457
	* Cloud SQL for PostgreSQL: Zonal - RAM in Americas $393
	* Storage PD Snapshot $155
	* [Billing – Cloud SQL](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;grouping=GROUP_BY_SKU;projects=holybricks;products=services%2F9662-B51E-5089?project=holybricks)
* Cloud Logging: $840
	* Log Storage cost $840
	* [Billing – Cloud Logging](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;grouping=GROUP_BY_SKU;projects=holybricks;products=services%2F5490-F7B7-8DF6?project=holybricks)
* Vertex AI: $725
	* обучение
* AppEngine: $709
	* бекапы firestore
	* [Billing – AppEngine](https://console.cloud.google.com/billing/01A1F6-85E6FA-B2E4D8/reports;grouping=GROUP_BY_SKU;projects=holybricks;products=services%2FF17B-412E-CB64?project=holybricks)
# Как адресуем
- [x] turnoff most unnecessary cronjobs + ml train
	- expected effect (-> $2K)
- [x] switch half of the cluster to preemptible nodes
	- expected effect $0.7-1K
- [x] switch / downscale test and ml Cloud SQL instances
	- expected effect $0.7-1K
	- [ ] maybe move dev cluster to neon tech
- [ ] поменять региональность бакетов с multi-region на single region
	- expected effect $400
- [x] перенести логи бекенда в хранилище с коротким ретеншном
	- expected effect $400-500
	- уменьшил ретеншн логов до 7 дней
	- перенес логи в loki
- [x] уменьшить ретеншн бекапов firestore
	- expected effect $300-500
- [ ] Оптимизировать ресурсы в кубере (возможно, включить VPA)
- [ ] Оптимизировать инстансы БД
# Что интересно
* Если не включать мозг и раскидать сервисы между разными `zone` в одном `region` то трафик будет стоить ощутимо $15-20/day
	* собрал весь кластер в `us-central1-a`
* Логи биллятся не за ретеншн (все что до 30 дней стоит одинаково, хоть 7, хоть 30), а биллятся за объем обработанных логов гугловым лог-процессингом
	* то есть, чтобы снизить кост, нужно не уменьшать ретеншн, а уменьшать количество логов которые пролетают через Log Router в обработку