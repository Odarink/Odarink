<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/card-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/card-light.svg">
  <img alt="Artem Kholdzhgonov, Senior Data Engineer, Moscow. Up to 2 terabytes ingested per day, 20 to 30 pipelines in production, about 100 users across 20 plus teams. Data flow: sources to warehouse to flows to marts to BI." src="assets/card-dark.svg">
</picture>

I take data from wherever it lives to wherever it can be analysed, and I measure the trip.
Five years across retail and banking.

### Where I've worked

- **Wildberries** — largest e-commerce marketplace in the CIS · Senior Data Engineer / Analyst · 2025 → now
  Up to 2 TB/day into ClickHouse, 20–30 Airflow DAGs in production, data serving 20+ teams (~100 analysts); Kafka, S3, PySpark.
- **Sber** — largest bank in Eastern Europe · Data Engineer, Middle+ · 2023–2025
  Consumer-credit risk marts on Greenplum and Hive/HDFS; data-quality tooling.
- **Promsvyazbank** — top-10 Russian bank · Lead Database Analyst · 2022–2023
  RAW → STG → DDS → CDM warehouse on MS SQL; Power BI and a Flask service.
- **LANIT** — one of the largest IT groups in Russia · Junior Data Engineer · 2021–2022
  Airflow ETL on PostgreSQL; API, FTP, HTTP and WFM sources.

### Selected work

**[csv_to_click](https://github.com/Odarink/csv_to_click)** — CSV into ClickHouse over an
HTTP-only path. 5.5 GB, 500M rows, 369.6 s.

- Profiling said per-row serialisation was 90% of insert time, not the network. Replacing it: 2.4×.
- Compression moved into the load workers, where zlib releases the GIL: 5.3× overall.
- Stopped there on arithmetic — producer 291 s and wire 368 s had converged, so nothing was left to win.
- 427 tests, green. Mutation testing and adversarial review caught the six defects they missed.

Rocket and impulse systems at BMSTU, then three years of self-taught Python — junior in 2021,
senior in 2025.

### Contact

[Telegram](https://t.me/Odarink) · [holdzhgonov.a@gmail.com](mailto:holdzhgonov.a@gmail.com) · English B2 · Open to remote & relocation
