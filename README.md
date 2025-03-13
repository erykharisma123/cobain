# ocr-service


### Setup Environment
Install [`uv`](https://docs.astral.sh/uv/getting-started/installation/) package manager
```shell
uv venv --python 3.12
uv sync
```

### Pytest
Run unit test
```shell
uv run pytest
```

### Code Lint and Formatter
Run `ruff`
```shell
uv run ruff check
```

### Migration
Create migration
```shell
alembic revision --autogenerate -m "new migration"
```

Run migration
```shell
alembic upgrade head
```

### Set Environment Variable
```shell
set -o allexport && source .env && set +o allexport
```

### Build Docker Images
```shell
export IMAGE_NAME="cdm-ocr-service"
export IMAGE_VERSION="1.0.0"
docker build . -t "${IMAGE_NAME}:${IMAGE_VERSION}"
```

### Run Local Development Server

To run this app locally, you need a Postgres database.
If you have Docker, you can start one with:

```shell
docker compose --env-file .env -f docker-compose.db_only.yaml up
```

Then run:

```shell
fastapi dev ocr_service/main.py
```

Visit [`http://localhost:8000/docs`](http://localhost:8000/docs) to see api docs!


### Docker Compose
Ensure the all the environment variables is properly configured.

Development mode
```shell
docker compose --env-file .env.docker -f docker-compose.dev.yaml up --build
```

Production mode
```shell
docker compose --env-file .env.docker -f docker-compose.prod.yaml up
```

### Sample Request
Request body to test the batch api
```json
{
  "callback_url": "http://0.0.0.0:8000/test/events/",
  "item_list": [
    {
        "reference_id": "307cf156dc-822e-4ed6-af4e-fdc55ea72568",
        "image_url": "https://storage.googleapis.com/chakra-loyalty/apiloyaltygcp/Production/upload/images/ocr/2024/11/20/307cf156dc-822e-4ed6-af4e-fdc55ea72568.jpg",
        "ocr_type": "RECEIPT"
    },
    {
        "reference_id": "30af8a5353-578d-4fb5-bdb0-1172c8a026fe",
        "image_url": "https://storage.googleapis.com/chakra-loyalty/apiloyaltygcp/Production/upload/images/ocr/2024/11/28/30af8a5353-578d-4fb5-bdb0-1172c8a026fe.jpeg",
        "ocr_type": "RECEIPT"
    },
    {
        "reference_id": "301cac2ab8-95bb-4db7-af78-cf60593734da",
        "image_url": "https://storage.googleapis.com/chakra-loyalty/apiloyaltygcp/Production/upload/images/ocr/2024/11/09/301cac2ab8-95bb-4db7-af78-cf60593734da.jpg",
        "ocr_type": "RECEIPT"
    }
  ]
}
```
