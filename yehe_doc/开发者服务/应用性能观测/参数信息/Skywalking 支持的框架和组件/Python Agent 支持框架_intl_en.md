This document lists the Python frameworks and components supported by APM.

| Project                                                         | Python Version - Lib Version                                       | Plugin Name            |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------ |
| [AIOHTTP](https://docs.aiohttp.org/)                         | Python >=3.10 - NOT SUPPORTED YET; Python >=3.6 - ['3.7.4']; | `sw_aiohttp`        |
| [Celery](https://docs.celeryproject.org/)                    | Python >=3.6 - ['5.1'];                                      | `sw_celery`         |
| [Django](https://www.djangoproject.com/)                     | Python >=3.6 - ['3.2'];                                      | `sw_django`         |
| [Elasticsearch](https://github.com/elastic/elasticsearch-py) | Python >=3.6 - ['7.13', '7.14', '7.15'];                     | `sw_elasticsearch`  |
| [Hug](https://falcon.readthedocs.io/en/stable/)              | Python >=3.10 - ['2.5', '2.6']; Python >=3.6 - ['2.4.1', '2.5', '2.6']; | `sw_falcon`         |
| [Flask](https://flask.palletsprojects.com/)                  | Python >=3.6 - ['1.1', '2.0'];                               | `sw_flask`          |
| [http.server](https://docs.python.org/3/library/http.server.html) | Python >=3.6 - ['*'];                                        | `sw_http_server`    |
| [Werkzeug](https://werkzeug.palletsprojects.com/)            | Python >=3.6 - ['1.0.1', '2.0'];                             | `sw_http_server`    |
| [kafka-python](https://kafka-python.readthedocs.io/)         | Python >=3.6 - ['2.0'];                                      | `sw_kafka`          |
| [psycopg-binary](https://www.psycopg.org/)                 | Python >=3.6 - ['3.0'];                                      | `sw_psycopg`        |
| [psycopg2-binary](https://www.psycopg.org/)                  | Python >=3.10 - NOT SUPPORTED YET; Python >=3.6 - ['2.9'];   | `sw_psycopg2`       |
| [PyMongo](https://pymongo.readthedocs.io/)                   | Python >=3.6 - ['3.11'];                                     | `sw_pymongo`        |
| [PyMySQL](https://pymysql.readthedocs.io/en/latest/)         | Python >=3.6 - ['1.0'];                                      | `sw_pymysql`        |
| [Pyramid](https://trypyramid.com/)                           | Python >=3.6 - ['1.10', '2.0'];                              | `sw_pyramid`        |
| [Pika](https://pika.readthedocs.io/)                         | Python >=3.6 - ['1.2'];                                      | `sw_rabbitmq`       |
| [Redis](https://github.com/andymccurdy/redis-py/)            | Python >=3.6 - ['3.5'];                                      | `sw_redis`          |
| [Requests](https://requests.readthedocs.io/en/master/)       | Python >=3.6 - ['2.26', '2.25'];                             | `sw_requests`       |
| [Sanic](https://sanic.readthedocs.io/en/latest)              | Python >=3.10 - NOT SUPPORTED YET; Python >=3.7 - ['20.12']; Python >=3.6 - ['20.12']; | `sw_sanic`          |
| [Tornado](https://www.tornadoweb.org/)                       | Python >=3.6 - ['6.0', '6.1'];                               | `sw_tornado`        |
| [urllib3](https://urllib3.readthedocs.io/en/latest/)         | Python >=3.6 - ['1.26', '1.25'];                             | `sw_urllib3`        |
| [urllib.request](https://docs.python.org/3/library/urllib.request.html) | Python >=3.6 - ['*'];                                        | `sw_urllib_request` |

>?The Celery server running "celery-A..." needs to run with the HTTP protocol, because Celery uses multiprocessing by default, which is incompatible with the current gRPC protocol implementation in SkyWalking.

