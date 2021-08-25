Документация по подключению к демо стенду Mailru IOT Platform
=============================================================


# Swagger specifications

Для каждого сервиса с публичным HTTP API к документации приложена swagger спецификация.

В каждом запросе к любому сервису необходимо указывать client_id тенанта, а также jwt токен, полученный в обмен на
креды в Keycloak.

## Registry

Хранилище метаинформации - транзакционное хранилище для всей метаинформации платформы.

Swagger спецификация приложена к документации `registry/swagger.json`

### Examples

Получение корневого тэга проекта:

```bash
    curl -s \
        -X GET 'https://iot.mcs.mail.ru/registry/v1/clients/{client_id}/root_tag' \
        --header "Authorization: Bearer {access_token}" \
        | jq
```

Получение первых 100 детей тэга:
```bash
    curl -s \
        -X GET 'https://iot.mcs.mail.ru/registry/v1/clients/{client_id}/tags/{tag_id}/children' \
        --header "Authorization: Bearer {access_token}" \
        | jq
```

## Digital Twins

Сервис цифровых двойников хранит текущее состояние подключённых устройств в памяти.

Swagger спецификация приложена к документации `digital-twins/swagger.json`

### Examples

Получение текущего состояния устройства:

```bash
    curl -s \
        -X GET 'https://iot.mcs.mail.ru/digital-twins/api/v1/clients/{client_id}/devices/{device_id}' \
        --header "Authorization: Bearer {access_token}" \
        | jq
```

## Operational Storage

Оперативное хранилище хранит показания датчиков, агрегаты и прочие данные типа timeseries в памяти 
за последние N часов (по умолчанию за сутки).

Swagger спецификация приложена к документации `operational-storage/swagger.json`

### Examples

Получение последнего значения тэга:
```bash
    curl -s \
        -X GET 'https://iot.mcs.mail.ru/operational-storage/api/v1/clients/{client_id}/query/events/latest?tag_id={tag_id}' \
        --header "Authorization: Bearer {access_token}" \
        | jq
```

## Long-term Storage

Долговременное хранилище на базе Clickhouse хранит показания датчиков, агрегаты и прочие данные типа timeseries за всё 
время, имеет http rest api схожий с оперативным хранилищем + доступны SQL запросы в сам Clickhouse.

Swagger спецификация приложена к документации `long-term-storage/swagger.json`

### Examples

Получение последнего значения тэга:
```bash
    curl -s \
        -X GET 'https://iot.mcs.mail.ru/long-term-storage/api/v1/clients/{client_id}/query/events/latest?tag_id={tag_id}' \
        --header "Authorization: Bearer {access_token}" \
        | jq
```

## HTTP Gateway

Swagger спецификация приложена к документации `http-gateway/swagger.json`
