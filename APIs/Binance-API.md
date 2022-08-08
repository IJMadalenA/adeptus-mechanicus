# Binance-API.

## Inicio.

```python
pip install binance-connector
```

Esta es la librería oficial de __Binance__ para Python.

https://github.com/binance/binance-connector-python

---

## [Base URL.](https://binance-connector.readthedocs.io/en/latest/getting_started.html#base-url)

el `base_url` no se provee pero por defecto es `api.binance.com`.

```python
from binance.spot import Spot as Client

client = Client(base_url='https://api.binance.com')
```

Es recomendado ingresar el parámetro `base_url` incluso en entornos de producción, ya que Binance proporciona `url` alternativas en caso de problemas de rendimiento:

- `https:\\api1.binance.com`
- `https:\\api2.binance.com`
- `https:\\api3.binance.com`

---

## [Endpoint Security type.](https://binance-docs.github.io/apidocs/spot/en/#endpoint-security-type)

- Each endpoint has a security type that determines how you will interact with it. This is stated next to the NAME of the endpoint.
  - If no security type is stated, assume the security type is NONE.
- API-keys are passed into the Rest API via the `X-MBX-APIKEY` header.
- API-keys and secret-keys **are case sensitive**.
- API-keys can be configured to only access certain types of secure endpoints. For example, one API-key could be used for TRADE only, while another API-key can access everything except for TRADE routes.
- By default, API-keys can access all secure routes.

| Security Type | Description                                              |
| :------------ | :------------------------------------------------------- |
| NONE          | Endpoint can be accessed freely.                         |
| TRADE         | Endpoint requires sending a valid API-Key and signature. |
| MARGIN        | Endpoint requires sending a valid API-Key and signature. |
| USER_DATA     | Endpoint requires sending a valid API-Key and signature. |
| USER_STREAM   | Endpoint requires sending a valid API-Key.               |
| MARKET_DATA   | Endpoint requires sending a valid API-Key.               |

- `TRADE`, `MARGIN` and `USER_DATA` endpoints are `SIGNED` endpoints.

---



---

## Error Codes.

https://binance-docs.github.io/apidocs/spot/en/#error-codes

## HTTP Return Codes.

- HTTP `4XX` return codes are used for malformed requests; the issue is on the sender's side.
- HTTP `403` return code is used when the WAF Limit (Web Application Firewall) has been violated.
- HTTP `429` return code is used when breaking a request rate limit.
- HTTP `418` return code is used when an IP has been auto-banned for continuing to send requests after receiving `429` codes.
- HTTP `5XX` return codes are used for internal errors; the issue is on Binance's side. It is important to **NOT** treat this as a failure operation; the execution status is **UNKNOWN** and could have been a success.

---

