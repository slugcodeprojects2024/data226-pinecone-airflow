# DATA 226 Pinecone Airflow Assignment

Airflow DAG `Medium_to_Pinecone` builds a semantic search engine over Medium article titles using Pinecone and sentence-transformers.

## 1. docker-compose.yaml changes

The `sentence-transformers` and `pinecone` packages were added to the Airflow containers in `docker-compose.yaml`:

```yaml
_PIP_ADDITIONAL_REQUIREMENTS: ${_PIP_ADDITIONAL_REQUIREMENTS:- sentence-transformers pinecone}
```

Containers were restarted with:

```bash
docker compose down
docker compose up -d
```

Screenshot: `screenshots/PackagesInstalled.png`

## 2. Pinecone configuration

- Created a Pinecone account and generated an API key.
- Stored the key as an Airflow Variable named `pinecone_api_key` (Admin, Variables).

Screenshot: `screenshots/AirflowVariable.png`

## 3. DAG run and task dependencies

DAG file: `dags/build_pinecone_search.py`

Task flow:

```
download_data -> preprocess_data ----\
                                       -> generate_embeddings_and_upsert -> test_search_query
create_pinecone_index ----------------/
```

Screenshots:
- `screenshots/DagGraph.png` (Graph view, all tasks successful)
- `screenshots/SearchResults.png` (test_search_query log)
- `screenshots/PineconeIndex.png` (index in Pinecone console)

## 4. Repository

This repository: <PASTE YOUR GITHUB REPO LINK HERE>
